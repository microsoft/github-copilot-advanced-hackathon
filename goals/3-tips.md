# Tips & Tricks for Spec-Driven Development with GitHub Copilot and Spec-Kit

## General Best Practices

- **Use Clear, Descriptive Prompts**  
  Frame your comments or stub code with precise intent to guide Copilot’s suggestions.
- **Iterate and Refine**  
  If the first suggestion isn’t ideal, use markdown files to work through the problem with the AI. Don't just assume it understands how to build good code, instruct it on how!
- **Leverage Context Blocks**  
  Provide related function signatures or comments so Copilot can infer correct patterns.
- **Approve Carefully**  
  Always review and test generated code; Copilot can sometimes hallucinate or suggest insecure patterns.
- **Combine with Documentation**  
  Remind the AI to reach out to Context7 on the regular to validate its thoughts and plans against real documentation.

## Workflow-Specific Tips for Spec-Kit

- **Follow the Core Spec-Kit Commands**  
  Use the provided Copilot slash commands in order: `/speckit.constitution` → `/speckit.specify` → `/speckit.clarify` → `/speckit.plan` → `/speckit.tasks` → `/speckit.implement`. This structured flow ensures Copilot has complete, consistent context at every stage.
- **Sync Specs After Major Changes**  
  After refactoring or architectural decisions, update your spec artifacts in `.specify/specs/` and re-run `/speckit.analyze` to catch drift before it compounds.
- **Document Decisions in constitution.md**  
  When you make architectural or implementation decisions, add them to `.specify/memory/constitution.md`. This keeps Copilot aligned with your project's principles across sessions.
- **Use Clarify Before Planning**  
  Always run `/speckit.clarify` before `/speckit.plan`. This lets Copilot surface ambiguities and edge cases that would otherwise become costly mid-implementation rework.
- **Update Specs When Reality Diverges**  
  If implementation reveals gaps in the spec, update the spec first, then re-run the affected phases. Specs are the source of truth.
- **Reset Context When Needed**  
  If Copilot starts to drift, start a new chat and re-run `/speckit.constitution` or reference your spec files directly to restore context.

### Key Spec-Kit Commands Reference

| Command | Purpose |
|---------|---------|
| `/speckit.constitution` | Establish project principles and governance |
| `/speckit.specify` | Create a feature specification from requirements |
| `/speckit.clarify` | Clarify underspecified areas (run before `/speckit.plan`) |
| `/speckit.plan` | Generate technical implementation plan |
| `/speckit.tasks` | Break implementation plan into actionable tasks |
| `/speckit.implement` | Execute tasks and build the feature |
| `/speckit.analyze` | Cross-artifact consistency & coverage analysis |
| `/speckit.checklist` | Generate quality checklists for requirements |

## Common Pitfalls to Avoid

- **Over-accepting Suggestions**  
  Blindly trusting suggestions can introduce bugs, security issues, or licensing conflicts.
- **Fragmented Context**  
  Jumping between files without context often leads to mismatched or incomplete code completions.
- **Static Imports Only**  
  Copilot might suggest unused imports; remove or consolidate imports to keep code clean.
- **Ignoring Edge Cases**  
  Generated code may skip error handling or boundary checks—always verify exceptional paths.
- **Outdated Context**  
  After refactoring, invalid or stale comments can mislead Copilot; update related comments and stubs.
- **Context overflow**  
  Reset the chat context often. Tell the AI to update the `.specify/memory/` files, then start a new chat. This can help if things go off the rails.

## Troubleshooting Scenarios

### 1. Suggestion Drift After Refactor
**Issue:** Copilot continues suggesting outdated patterns post-refactor.
**Resolution:**  
- Update in-file comments to reflect new APIs or signatures.  
- Restart your IDE or clear Copilot cache if issues persist.

### 2. Performance Hangs on Large Files
**Issue:** Autocomplete lags in big modules.
**Resolution:**  
- Split large files into smaller, focused modules.  
- Disable Copilot in specific file types if not needed.

### 3. Incorrect Language Features
**Issue:** Copilot suggests syntax not supported by your project’s runtime or compiler.
**Resolution:**  
- Specify target language version in comments or config.  
- Add a small code comment with `// @ts-check` or similar hints.

### 4. Licensing or Legal Worries
**Issue:** Concern over code origin or license compatibility.
**Resolution:**  
- Vet suggestions for existing licenses.  
- Find, specify, and instruct which packages you want allowed!

### 5. Missing Dependencies
**Issue:** Suggestions reference packages not installed.
**Resolution:**  
- Preemptively install common dependencies.  
- Add an import stub comment (e.g., `import { } from 'lodash';`) to guide Copilot.

---

*These tips aim to empower your Spec-Driven Development experience with Spec-Kit and help you avoid common frustrations. Happy coding!*
