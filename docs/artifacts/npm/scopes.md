---
title: Use npm scopes for private packages
description: Use npm scopes for private packages in Azure DevOps Services
ms.assetid: c88868bd-8101-48f3-b76d-17c858181fda
ms.technology: devops-artifacts
ms.topic: conceptual
ms.date: 04/30/2020
monikerRange: ">= tfs-2017"
---

# Use npm scopes

**Azure DevOps Services** | **TFS 2018** | **TFS 2017**

[Scopes](https://docs.npmjs.com/misc/scope) are built into npm and are a way of grouping packages together.
In Azure DevOps Services and in npmjs.com, you can publish and use both scoped and unscoped packages.

A scope allows you to create a package with the same name as a package created by another user or Org without conflict.
They allow the user to separate public and private packages by prefixing their packages with a scope `@fabrikam` and configuring the `.npmrc` file to only use an Azure Artifacts feed for that scope.

> [!NOTE]
> In order to use scopes you must be using npm version 2 or greater. Run `npm install npm@latest -g` on the command line to upgrade to the latest version.

## Set up

To use an Azure Artifacts feed with a scope, follow the instructions below, but append your scope to both lines in the project `.npmrc` file.

[!INCLUDE [](../includes/npm/npmrc.md)]

Then, replace:

- `registry=<your feed URL>` with
- `@fabrikam:registry=<your feed URL>`

> [!NOTE]
> Make sure you add the scope and package names to your `package.json` file: `{ "name": "@fabrikam/package-name" }`.

## Upstreams or scopes?

Scopes add an additional restriction when naming your packages: each package name must start with `@<scope>`. If you're ok with this limitation, and don't intend to ever publish your private packages to npmjs.com, scopes are an alternative to [upstream sources](upstream-sources.md).

If you do intend to publish private packages to npmjs.com, we recommend not using scopes unless you intend to publish your packages to npmjs.com with the scope intact; if you remove the scope when transitioning the package from Azure Artifacts to npmjs.com, you'll need to update any package.json references accordingly.
