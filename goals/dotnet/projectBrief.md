# Project Brief: eShop (.NET Reference Application)

## Overview
The **eShop** project is a reference .NET application developed by the .NET team to demonstrate modern application architecture and development practices using the latest .NET technologies. It implements a full-featured e-commerce website and serves as a practical example for developers building cloud-native, scalable, and maintainable applications.

## Purpose
The primary goals of the eShop project are to:
- Showcase best practices in .NET application development.
- Demonstrate the use of **.NET Aspire**, a new stack for building distributed applications.
- Provide a hands-on learning tool for developers exploring microservices, containerization, and modern frontend/backend integration.

## Key Features
- **Architecture**: Services-based architecture using .NET Aspire.
- **Frontend**: Built with Blazor WebAssembly and ASP.NET Core.
- **Backend**: Includes APIs, microservices, and integration with databases and messaging systems.
- **DevOps Ready**: Includes CI/CD pipelines and Docker support.
- **AI Integration**: Features an AI-powered chatbot to assist users in product discovery and shopping.
- **Performance Optimizations**:
  - Uses `MapStaticAssets` for optimized static file handling.
  - Implements Brotli compression and fingerprinted file names for aggressive caching.

## Technology Stack
- .NET 9 (latest version)
- ASP.NET Core
- Blazor
- Docker
- Visual Studio 2022+
- Optional: .NET MAUI for cross-platform client apps

## Getting Started
To run the eShop project:
1. Clone the repository: [github.com/dotnet/eshop](https://github.com/dotnet/eshop)
2. Install prerequisites:
   - .NET 9 SDK
   - Visual Studio 2022 (with ASP.NET and .NET Aspire workloads)
   - Docker Desktop
3. Run the solution using Visual Studio or configure your environment using the provided PowerShell scripts.

## Internal Use and Demonstrations
The eShop app has been featured in internal presentations such as the `[dotnet conf 2024 Keynote - Copy 3](https://microsoft.sharepoint.com/teams/DevRelTeam/_layouts/15/Doc.aspx?sourcedoc=%7B15D653EE-CFB6-4C32-8669-EF8B2367FE95%7D&file=dotnet%20conf%202024%20Keynote%20-%20Copy%203.pptx&action=edit&mobileredirect=true&DefaultItemOpen=1&EntityRepresentationId=421e3d07-d5fd-4cc9-b4ee-9dac667e0f4b)`, where it was used to demonstrate .NET 9