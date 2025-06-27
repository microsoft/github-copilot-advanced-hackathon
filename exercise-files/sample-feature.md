# Feature: Loyalty Program – Points-Based Rewards System with Tier Benefits

## 📖 Executive Summary

### Business Value
- **Problem Statement**: eShop currently lacks a customer loyalty mechanism, resulting in lower repeat purchase rates and limited customer engagement. A loyalty program incentivizes users to return, increases average order value, and differentiates eShop from competitors.
- **Target Users**: Registered eShop customers (shoppers), marketing team (for campaigns), customer support (for issue resolution).

### Technical Alignment
- **Architecture Fit**: Follow microservices principles; encapsulate loyalty logic in a dedicated service. Integrate with Ordering, Catalog, and Identity services via events and APIs.
- **Service Boundaries**: New `Loyalty.API` microservice. Impacts Ordering.API (order completion), Identity.API (user profile), WebApp (UI integration), and potentially Catalog.API (reward-eligible products).
- **Data Ownership**: Loyalty.API owns all loyalty program data (points, tiers, transactions, rewards). Ordering and Identity services reference loyalty data via APIs/events.

## 🎯 Feature Requirements

### Functional Requirements
1. **LOY-1**: Award points for completed purchases
   - **Acceptance Criteria**:
     - Given a user completes an order,
     - When the order is marked as paid,
     - Then the user receives points based on order value and current promotions.

2. **LOY-2**: Support tiered membership (e.g., Bronze, Silver, Gold, Platinum)
   - **Acceptance Criteria**:
     - Given a user's cumulative points cross a tier threshold,
     - When the next order is completed,
     - Then the user's tier is upgraded and benefits are applied.

3. **LOY-3**: Allow users to view points balance, tier, and history
   - **Acceptance Criteria**:
     - Given a logged-in user,
     - When they access the loyalty dashboard,
     - Then they see current points, tier, and transaction history.

4. **LOY-4**: Enable points redemption for rewards (discounts, products, vouchers)
   - **Acceptance Criteria**:
     - Given a user has sufficient points,
     - When they choose a reward to redeem,
     - Then points are deducted and the reward is issued.

5. **LOY-5**: Admin management of loyalty rules, tiers, and promotions
   - **Acceptance Criteria**:
     - Given an admin user,
     - When they update rules or promotions,
     - Then changes are reflected in the loyalty program logic.

6. **LOY-6**: Notify users of tier upgrades and expiring points
   - **Acceptance Criteria**:
     - Given a user is upgraded or points are expiring soon,
     - When the event occurs,
     - Then the user receives an email or in-app notification.

### Non-Functional Requirements
- **Security**: Only authenticated users can access/modify their loyalty data. Admin APIs require elevated permissions. Prevent points fraud.
- **Usability**: Intuitive dashboard, clear tier progress, accessible on web/mobile.

## 🏗️ Technical Design

### Service Architecture
- **New Services**:
  - `Loyalty.API`: RESTful microservice for all loyalty operations (points, tiers, rewards, admin management).
- **Modified Services**:
  - `Ordering.API`: Publishes `OrderCompleted` events; consumes loyalty API for points awarding.
  - `Identity.API`: Optionally displays loyalty status in user profile.
  - `WebApp`: Integrates loyalty dashboard and redemption UI.
- **Service Communication**:
  - **Sync**: WebApp/Identity calls Loyalty.API for user data.
  - **Async**: Ordering.API emits `OrderCompleted` event; Loyalty.API subscribes and processes points.
- **Data Flow**:
  1. User completes order → Ordering.API emits event
  2. Loyalty.API processes event, updates points/tier
  3. User queries dashboard → WebApp fetches from Loyalty.API
  4. Redemption request → Loyalty.API validates, updates, issues reward

### Database Design
- **New Tables/Collections** (PostgreSQL):
  - `LoyaltyAccounts` (UserId PK, Points, Tier, LastActivity, CreatedAt)
  - `LoyaltyTransactions` (Id PK, UserId FK, Type [Earn/Spend/Adjust], Points, OrderId, Timestamp, Description)
  - `LoyaltyTiers` (TierId PK, Name, MinPoints, Benefits, Icon)
  - `LoyaltyRewards` (RewardId PK, Name, PointsRequired, Type [Discount/Product/Voucher], Details, Active)
  - `LoyaltyRedemptions` (RedemptionId PK, UserId FK, RewardId FK, PointsSpent, Status, CreatedAt, FulfilledAt)
  - `LoyaltyPromotions` (PromotionId PK, Name, Multiplier, StartDate, EndDate, Active)
  - Utilize EnumToString conversion for enums in Context definition
- **Data Relationships**:
  - 1:N from LoyaltyAccounts to LoyaltyTransactions and LoyaltyRedemptions
  - LoyaltyTiers referenced by LoyaltyAccounts
  - LoyaltyRewards referenced by LoyaltyRedemptions
- **Migration Strategy**:
  - Add new schema via migration scripts. Backfill existing users with default loyalty accounts.

### Event Design
- **Domain Events**:
  - `PointsAwarded`, `TierUpgraded`, `PointsRedeemed`, `PointsExpired`, `RewardIssued`
- **Integration Events**:
  - `OrderCompleted` (from Ordering.API)
  - `UserRegistered` (optional, for onboarding bonus)
- **Event Handlers**:
  - Loyalty.API background worker for event processing (idempotent, retry on failure)
  - Notification handler for user alerts

### API Design
```
# Loyalty API Endpoints
GET    /api/loyalty/account/{userId}           # Get points, tier, history
POST   /api/loyalty/redeem                     # Redeem points for reward
GET    /api/loyalty/tiers                      # List available tiers
GET    /api/loyalty/rewards                    # List available rewards
POST   /api/loyalty/admin/rules                # Update rules/promotions (admin)
POST   /api/loyalty/admin/tier                 # Create/update tier (admin)
POST   /api/loyalty/admin/reward               # Create/update reward (admin)

# Event Subscription
POST   /events/order-completed                 # (internal) handle order event
```

#### Proposed Class Definitions (C#)

```csharp
// Loyalty Domain
public class LoyaltyAccount {
    public Guid UserId { get; set; }
    public int Points { get; set; }
    public string Tier { get; set; }
    public DateTime LastActivity { get; set; }
    public List<LoyaltyTransaction> Transactions { get; set; }
}

public class LoyaltyTransaction {
    public Guid Id { get; set; }
    public Guid UserId { get; set; }
    public LoyaltyTransactionType Type { get; set; } // Earn, Spend, Adjust
    public int Points { get; set; }
    public Guid? OrderId { get; set; }
    public DateTime Timestamp { get; set; }
    public string Description { get; set; }
}

public enum LoyaltyTransactionType {
  Earn,
  Spend,
  Adjust
}

public class LoyaltyTier {
    public string Name { get; set; }
    public int MinPoints { get; set; }
    public string Benefits { get; set; }
    public string Icon { get; set; }
}

public class LoyaltyReward {
    public Guid RewardId { get; set; }
    public string Name { get; set; }
    public int PointsRequired { get; set; }
    public LocaltyRewardType Type { get; set; } // Discount, Product, Voucher
    public string Details { get; set; }
    public bool Active { get; set; }
}

public enum LoyaltyRewardType {
  Discount,
  Product,
  Voucher
}

public class LoyaltyRedemption {
    public Guid RedemptionId { get; set; }
    public Guid UserId { get; set; }
    public Guid RewardId { get; set; }
    public int PointsSpent { get; set; }
    public RedemptionStatus Status { get; set; } // Pending, Fulfilled, Cancelled
    public DateTime CreatedAt { get; set; }
    public DateTime? FulfilledAt { get; set; }
}

public enum RedemptionStatus {
  Pending,
  Fulfilled,
  Cancelled
}

// Interfaces
public interface ILoyaltyService {
    LoyaltyAccount GetAccount(Guid userId);
    void AwardPoints(Guid userId, int points, Guid? orderId = null);
    void RedeemPoints(Guid userId, Guid rewardId);
    void UpgradeTier(Guid userId);
    IEnumerable<LoyaltyTier> GetTiers();
    IEnumerable<LoyaltyReward> GetRewards();
}

public interface ILoyaltyAdminService {
    void UpdateRules(LoyaltyRules rules);
    void CreateOrUpdateTier(LoyaltyTier tier);
    void CreateOrUpdateReward(LoyaltyReward reward);
}

// Business Logic (examples)
public void AwardPoints(Guid userId, int points, Guid? orderId = null) {
    // 1. Fetch LoyaltyAccount
    // 2. Add points, create LoyaltyTransaction
    // 3. Check for tier upgrade
    // 4. Emit PointsAwarded, TierUpgraded events if needed
}

public void RedeemPoints(Guid userId, Guid rewardId) {
    // 1. Validate points balance
    // 2. Deduct points, create LoyaltyRedemption
    // 3. Issue reward, emit PointsRedeemed, RewardIssued events
}
```

## 🔄 Implementation Roadmap

### Phase 1: Foundation (Week 1-2)
- [ ] Create Unit tests with xunit
- [ ] Scaffold Loyalty.API microservice
- [ ] Define database schema and migrations
- [ ] Implement basic CRUD for accounts, tiers, rewards

### Phase 2: Core Features (Week 3-4)
- [ ] Integrate with Ordering.API events
- [ ] Implement points awarding and tier logic
- [ ] Build user dashboard endpoints
- [ ] Implement admin management APIs

### Phase 3: Integration (Week 5-6)
- [ ] Integrate with WebApp UI (dashboard, redemption)
- [ ] Add notifications for upgrades/expiring points
- [ ] End-to-end and integration testing

### Phase 4: Polish (Week 7-8)
- [ ] Performance optimization and caching
- [ ] Security review and hardening
- [ ] Documentation and user guides

## 🧪 Testing Strategy

### Unit Testing
- [ ] Loyalty points calculation logic
- [ ] Tier upgrade logic
- [ ] Redemption validation
- [ ] Admin rule changes

### Integration Testing
- [ ] API endpoint tests (CRUD, dashboard, redemption)
- [ ] Event handler tests (order completed, points awarded)
- [ ] Database integration and migration tests

### End-to-End Testing
- [ ] User workflow: earn, view, redeem, upgrade
- [ ] Admin workflow: manage rules, tiers, rewards
- [ ] Performance and load tests

## 📊 Monitoring & Observability

### Metrics
- [ ] Points awarded per day/week
- [ ] Tier upgrade rates
- [ ] Redemption rates and reward popularity
- [ ] API latency and error rates

### Logging
- [ ] Structured logs for all loyalty transactions
- [ ] Correlation IDs for event-driven flows
- [ ] Security audit logs for admin actions

### Alerting
- [ ] Failed event processing
- [ ] Redemption failures
- [ ] Unusual points activity (fraud detection)

## 🚨 Risk Assessment

### Technical Risks
- **Risk**: Eventual consistency between Ordering and Loyalty (delayed points)
  - **Probability**: Medium
  - **Impact**: Medium
  - **Mitigation**: Idempotent event handling, user messaging
- **Risk**: Points fraud or abuse
  - **Probability**: Low
  - **Impact**: High
  - **Mitigation**: Validation, audit logs, anomaly detection
- **Risk**: Performance bottlenecks at scale
  - **Probability**: Medium
  - **Impact**: Medium
  - **Mitigation**: Caching, async processing, DB indexing

### Business Risks
- **Risk**: Low user adoption
  - **Mitigation**: Marketing campaigns, onboarding bonuses
- **Risk**: Reward cost overruns
  - **Mitigation**: Dynamic reward management, analytics

## 🎓 Decision Log

### Decision 1: Microservice vs. Monolith for Loyalty
- **Context**: Where to implement loyalty logic
- **Options Considered**: Integrate into Ordering.API vs. new Loyalty.API
- **Decision**: New Loyalty.API microservice
- **Rationale**: Separation of concerns, scalability, future extensibility
- **Consequences**: Additional deployment, but better maintainability

### Decision 2: Event-Driven Points Awarding
- **Context**: How to trigger points for orders
- **Options Considered**: Synchronous API call vs. event subscription
- **Decision**: Subscribe to OrderCompleted events
- **Rationale**: Decouples services, resilient to failures
- **Consequences**: Eventual consistency, requires idempotency

## 📚 References

- [Microsoft DDD eShop Reference](https://github.com/dotnet-architecture/eShopOnContainers)
- [Event-Driven Architecture Patterns](https://docs.microsoft.com/azure/architecture/patterns/event-driven-architecture)
- [CQRS and Event Sourcing](https://docs.microsoft.com/azure/architecture/patterns/cqrs)
- [Loyalty Program Best Practices](https://www.shopify.com/enterprise/loyalty-programs)
- [OpenAPI Specification](https://swagger.io/specification/)