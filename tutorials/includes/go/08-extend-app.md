---
ms.localizationpriority: medium
---

<!-- markdownlint-disable MD041 -->

In this section you will add your own Microsoft Graph capabilities to the application. This could be a code snippet from Microsoft Graph [documentation](/graph/api/overview) or [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer), or code that you created. This section is optional.

[!INCLUDE [preview-disclaimer](preview-disclaimer.md)]

## Update the app

1. Add the following function to **./graphhelper/graphhelper.go**.

    :::code language="go" source="./src/user-auth/graphtutorial/graphhelper/graphhelper.go" id="MakeGraphCallSnippet":::

1. Replace the empty `makeGraphCall` function in **graphtutorial.go** with the following.

    :::code language="go" source="./src/user-auth/graphtutorial/graphtutorial.go" id="MakeGraphCallSnippet":::

## Choose an API

Find an API in Microsoft Graph you'd like to try. For example, the [Create event](/graph/api/user-post-events) API. You can use one of the examples in the API documentation, or you can customize an API request in Graph Explorer and use the generated snippet.

## Configure permissions

Check the **Permissions** section of the reference documentation for your chosen API to see which authentication methods are supported. Some APIs don't support app-only, or personal Microsoft accounts, for example.

- To call an API with user authentication (if the API supports user (delegated) authentication), add the required permission scope in **.env** (or **.env.local**).
- To call an API with app-only authentication see the [app-only authentication](/graph/tutorials/go-app-only) tutorial.

## Add your code

Copy your code into the `MakeGraphCall` function in **graphhelper.go**. If you're copying a snippet from documentation or Graph Explorer, be sure to rename the `GraphServiceClient` to `userClient`.
