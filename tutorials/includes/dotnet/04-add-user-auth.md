---
ms.localizationpriority: medium
---

<!-- markdownlint-disable MD041 -->

In this section you will extend the application from the previous exercise to support authentication with Azure AD. This is required to obtain the necessary OAuth access token to call the Microsoft Graph. In this step you will integrate the [Azure Identity client library for .NET](https://www.nuget.org/packages/Azure.Identity) into the application and configure authentication for the [Microsoft Graph .NET client library](https://github.com/microsoftgraph/msgraph-sdk-dotnet).

The Azure Identity library provides a number of `TokenCredential` classes that implement OAuth2 token flows. The Microsoft Graph client library uses those classes to authenticate calls to Microsoft Graph.

## Configure Graph client for user authentication

In this section you will use the `DeviceCodeCredential` class to request an access token by using the [device code flow](/azure/active-directory/develop/v2-oauth2-device-code).

1. Create a new file in the **GraphTutorial** directory named **GraphHelper.cs** and add the following code to that file.

    ```csharp
    using Azure.Core;
    using Azure.Identity;
    using Microsoft.Graph;

    class GraphHelper
    {
    }
    ```

1. Add the following code to the `GraphHelper` class.

    :::code language="csharp" source="./src/user-auth/GraphTutorial/GraphHelper.cs" id="UserAuthConfigSnippet":::

1. Replace the empty `InitializeGraph` function in **Program.cs** with the following.

    :::code language="csharp" source="./src/user-auth/GraphTutorial/Program.cs" id="InitializeGraphSnippet":::

This code declares two private properties, a `DeviceCodeCredential` object and a `GraphServiceClient` object. The `InitializeGraphForUserAuth` function creates a new instance of `DeviceCodeCredential`, then uses that instance to create a new instance of `GraphServiceClient`. Every time an API call is made to Microsoft Graph through the `_userClient`, it uses the provided credential to get an access token.

## Test the DeviceCodeCredential

Next, add code to get an access token from the `DeviceCodeCredential`.

1. Add the following function to the `GraphHelper` class.

    :::code language="csharp" source="./src/user-auth/GraphTutorial/GraphHelper.cs" id="GetUserTokenSnippet":::

1. Replace the empty `DisplayAccessTokenAsync` function in **Program.cs** with the following.

    :::code language="csharp" source="./src/user-auth/GraphTutorial/Program.cs" id="DisplayAccessTokenSnippet":::

1. Build and run the app. Enter `1` when prompted for an option. The application displays a URL and device code.

    ```Shell
    .NET Graph Tutorial

    Please choose one of the following options:
    0. Exit
    1. Display access token
    2. List my inbox
    3. Send mail
    4. Make a Graph call
    1
    To sign in, use a web browser to open the page https://microsoft.com/devicelogin and
    enter the code RB2RUD56D to authenticate.
    ```

1. Open a browser and browse to the URL displayed. Enter the provided code and sign in.

    [!INCLUDE [browser-auth-note](../shared/browser-auth-note.md)]

1. Once completed, return to the application to see the access token.

    [!INCLUDE [token-debug-tip](../shared/token-debug-tip.md)]
