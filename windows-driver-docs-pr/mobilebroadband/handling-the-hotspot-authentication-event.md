---
title: 处理热点身份验证事件
description: 处理热点身份验证事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c24a5a4a755dc865c12d1b0e4494cdae798b3a6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782323"
---
# <a name="handling-the-hotspot-authentication-event"></a>处理热点身份验证事件


Windows 8、Windows 8.1 和 Windows 10 在检测到支持无线 Internet 服务提供商漫游 (WISPr) 的捕获门户时，会触发热点身份验证事件。

事件发生时，接收应用程序必须使用作为参数提供给事件处理程序的事件标记立即调用 [**NetworkOperator. HotspotAuthentication. TryGetAuthenticationContext**](/uwp/api/Windows.Networking.NetworkOperators.HotspotAuthenticationContext#Windows_Networking_NetworkOperators_HotspotAuthenticationContext_TryGetAuthenticationContext_System_String_Windows_Networking_NetworkOperators_HotspotAuthenticationContext__) 函数。 此函数返回一个对象，该对象管理热点身份验证尝试。 当函数失败时，事件处理程序必须退出，而不执行任何其他操作。

对象上的属性允许你的应用程序检索以下项：

-   无线网络的 SSID。

-   有关连接到热点的网络适配器的详细信息。

-   包含 WISPr 消息的 URL。

-   WISPr 消息的 XML 负载。

-   提供凭据的身份验证 URL。

存在其他 Api 来检索以下项：

-   无线网络的 BSSID (参阅) 的 [**Windows 网络连接命名空间**](/uwp/api/Windows.Networking.Connectivity) 。

-   网络的 DHCP 参数 (参阅) [的 UWP 应用的 Win32 和 COM](/uwp/win32-and-com/win32-and-com-for-uwp-apps) 。

通过使用此信息以及你的应用程序需要从本地系统或网络获取的任何其他信息，可以生成凭据。 对象还包含允许应用继续或完成热点身份验证的方法。

本主题中提供了以下各节：

-   [颁发凭据](#issuecred)

-   [中止身份验证](#abortauth)

-   [使用备用身份验证方法](#altauth)

-   [与用户交互](#userint)

## <a name="span-idissuecredspanspan-idissuecredspanissue-credentials"></a><span id="issuecred"></span><span id="ISSUECRED"></span>颁发凭据


在最简单的情况下，应用将根据其具有或可检索到的信息生成凭据。 例如，使用 WISPr 有效负载中的信息生成用户名和密码以及有关网络适配器的信息。

执行任何必要的操作来生成或获取凭据后，应用程序将对 [**HotspotAuthenticationContext**](/uwp/api/Windows.Networking.NetworkOperators.HotspotAuthenticationContext)对象调用 [**IssueCredentials**](/uwp/api/Windows.Networking.NetworkOperators.HotspotAuthenticationContext#Windows_Networking_NetworkOperators_HotspotAuthenticationContext_IssueCredentials_System_String_System_String_System_String_System_Boolean_)方法。 此方法允许应用提供以下内容：

-   WISPr *用户名* 参数

-   WISPr *密码* 参数

-   要包括在 WISPr 响应中的任意非标准参数

-   失败时的行为

如果服务器拒绝应用提供的凭据，Windows 将从网络断开连接，并且不会重试当前用户会话中的连接。 最终标志允许应用程序指出如果凭据不成功，则 Windows 不应使用此配置文件自动重试连接。

此 API 有两种变体。 [**IssueCredentials**](/uwp/api/Windows.Networking.NetworkOperators.HotspotAuthenticationContext#Windows_Networking_NetworkOperators_HotspotAuthenticationContext_IssueCredentials_System_String_System_String_System_String_System_Boolean_)方法将参数传递给 Windows，然后立即返回。 此 API 不提供身份验证尝试的结果。 Windows 8.1 中引入的 [**IssueCredentialsAsync**](/uwp/api/Windows.Networking.NetworkOperators.HotspotAuthenticationContext#Windows_Networking_NetworkOperators_HotspotAuthenticationContext_IssueCredentialsAsync_System_String_System_String_System_String_System_Boolean_) 方法是允许应用程序检索身份验证尝试结果的异步版本。

## <a name="span-idabortauthspanspan-idabortauthspanabort-authentication"></a><span id="abortauth"></span><span id="ABORTAUTH"></span>中止身份验证


如果应用发现无法为当前网络生成凭据 (因为漫游协议已更改、信息不可用，或者出于其他原因) ，则它必须对 [**HotspotAuthenticationContext**](/uwp/api/Windows.Networking.NetworkOperators.HotspotAuthenticationContext)对象调用 [**AbortAuthentication**](/uwp/api/Windows.Networking.NetworkOperators.HotspotAuthenticationContext#Windows_Networking_NetworkOperators_HotspotAuthenticationContext_AbortAuthentication_System_Boolean_)方法。

Windows 断开与网络的连接，并且不会重新尝试当前用户会话中的连接。 此函数接受一个标志，该标志指示 Windows 绝不应使用此配置文件自动重试连接。

**注意**  
此方法不会从系统中删除配置文件，如果用户手动尝试连接到网络，则可能会再次要求该应用提供凭据。 如果已完全删除该配置文件，则该应用必须提供一个新的预配文件，该文件将删除相关的配置文件。

 

## <a name="span-idaltauthspanspan-idaltauthspanuse-alternate-authentication-methods"></a><span id="altauth"></span><span id="ALTAUTH"></span>使用备用身份验证方法


如果应用可以使用 WISPr 以外的方法进行身份验证，则可能需要这样做。 使用备用方法成功向网络进行身份验证后，必须通过对 [**HotspotAuthenticationContext**](/uwp/api/Windows.Networking.NetworkOperators.HotspotAuthenticationContext)对象调用 [**SkipAuthentication**](/uwp/api/Windows.Networking.NetworkOperators.HotspotAuthenticationContext#Windows_Networking_NetworkOperators_HotspotAuthenticationContext_SkipAuthentication)方法来完成连接。 调用此方法时，Windows 将重新检测与 Internet 的连接，从而帮助用户界面 (UI) 正确反映身份验证状态。

**注意**  
对于不为 WISPr 协议提供支持的热点，不会调用 HotspotAuthentication 事件。 但是，这允许应用程序选择要在响应中使用的其他协议，或在需要时使用自定义的 WISPr 版本。

 

## <a name="span-iduserintspanspan-iduserintspaninteract-with-the-user"></a><span id="userint"></span><span id="USERINT"></span>与用户交互


如果在进行身份验证之前需要用户交互，则应用必须对 [**HotspotAuthenticationContext**](/uwp/api/Windows.Networking.NetworkOperators.HotspotAuthenticationContext)对象调用 [**TriggerAttentionRequired**](/uwp/api/Windows.Networking.NetworkOperators.HotspotAuthenticationContext#Windows_Networking_NetworkOperators_HotspotAuthenticationContext_TriggerAttentionRequired_System_String_System_String_)方法。 此方法在以下情况下很有用：

-   用户选择不在应用中存储凭据，必须登录。

-   完成连接将对用户的信用卡或其他帐户收费;因此，在继续操作之前需要同意。

-   用户帐户没有信用额度，需要新的购买。

此方法不会完成身份验证。 调用此方法时，将使用指定的参数在前台打开应用请求。 应将事件标记传递到前台应用程序，以便它可以再次检索 [**HotspotAuthenticationContext**](/uwp/api/Windows.Networking.NetworkOperators.HotspotAuthenticationContext) 对象并使用其他三种方法之一完成身份验证。

不保证应用程序在前台打开的请求已成功。 当计算机处于连接待机状态时，自动连接可能会导致 HotspotAuthentication 事件。 仅当计算机不再处于连接状态的情况下，该应用程序才会启动，已解除锁定并且仍连接到无线网络。 由于这会在用户解锁计算机之前延迟 Internet 访问，因此，只要可以自动生成凭据，就应该避免此状态。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[WISPr 身份验证](wispr-authentication.md)

 

