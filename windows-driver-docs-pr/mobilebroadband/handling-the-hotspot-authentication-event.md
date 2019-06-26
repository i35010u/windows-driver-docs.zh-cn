---
title: 处理热点身份验证事件
description: 处理热点身份验证事件
ms.assetid: e293757e-de4b-4669-a6c4-a57fff157cf4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b1111ab3857071d6c98eb40366c594ff9926bf9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381467"
---
# <a name="handling-the-hotspot-authentication-event"></a>处理热点身份验证事件


Windows 8、 Windows 8.1 和 Windows 10 中触发热点身份验证事件检测到一个强制网络门户，支持无线 Internet 服务提供商时漫游 (WISPr)。

事件发生时，接收应用程序必须立即调用[ **Windows.Networking.NetworkOperator.HotspotAuthentication.TryGetAuthenticationContext** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.HotspotAuthenticationContext#Windows_Networking_NetworkOperators_HotspotAuthenticationContext_TryGetAuthenticationContext_System_String_Windows_Networking_NetworkOperators_HotspotAuthenticationContext__)函数通过使用事件标记作为事件处理程序的参数提供。 此函数返回管理热点身份验证尝试的对象。 在的函数失败，事件处理程序必须退出而不执行任何其他操作。

对象的属性允许您的应用程序检索以下各项：

-   无线网络的 SSID。

-   有关连接到热点的网络适配器的详细信息。

-   包含 WISPr 消息的 URL。

-   WISPr 消息 XML 负载。

-   向其提供凭据身份验证 URL。

其他 Api 存在检索以下各项：

-   无线网络的 BSSID (请参阅[ **Windows.Networking.Connectivity 命名空间**](https://docs.microsoft.com/uwp/api/Windows.Networking.Connectivity))。

-   网络的 DHCP 参数 (请参阅[Win32 和 COM 适用于 UWP 应用](https://docs.microsoft.com/uwp/win32-and-com/win32-and-com-for-uwp-apps))。

通过使用此信息和您的应用程序需要从本地系统或网络获取任何其他信息，可生成凭据。 该对象还包含允许应用程序以继续或完成热点身份验证的方法。

本主题中提供了以下各节：

-   [问题凭据](#issuecred)

-   [中止身份验证](#abortauth)

-   [使用备用身份验证方法](#altauth)

-   [与用户交互](#userint)

## <a name="span-idissuecredspanspan-idissuecredspanissue-credentials"></a><span id="issuecred"></span><span id="ISSUECRED"></span>问题凭据


在最简单的情况下，应用会生成基于的信息已或可以检索凭据。 例如，用户名和密码生成使用 WISPr 有效负载中的信息和有关网络适配器的信息。

在执行后生成或获取凭据所需的任何操作，该应用程序调用[ **IssueCredentials** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.HotspotAuthenticationContext#Windows_Networking_NetworkOperators_HotspotAuthenticationContext_IssueCredentials_System_String_System_String_System_String_System_Boolean_)方法[ **HotspotAuthenticationContext**](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.HotspotAuthenticationContext)对象。 此方法允许应用提供以下：

-   WISPr*用户名*参数

-   WISPr*密码*参数

-   若要在 WISPr 响应中包含的任意非标准参数

-   失败的行为

如果服务器将拒绝应用程序提供的凭据，Windows 将从网络断开连接，并不会重试中当前用户会话的连接。 最终标志允许应用程序以指明，是否凭据不成功，Windows 应永远不会自动重试连接使用此配置文件。

有两种变体，此 api。 [ **IssueCredentials** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.HotspotAuthenticationContext#Windows_Networking_NetworkOperators_HotspotAuthenticationContext_IssueCredentials_System_String_System_String_System_String_System_Boolean_)方法会将参数传递到 Windows，然后立即返回。 此 API 不提供身份验证尝试的结果。 [ **IssueCredentialsAsync** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.HotspotAuthenticationContext#Windows_Networking_NetworkOperators_HotspotAuthenticationContext_IssueCredentialsAsync_System_String_System_String_System_String_System_Boolean_) Windows 8.1 中引入的方法是使应用程序以检索身份验证尝试的结果的异步版本。

## <a name="span-idabortauthspanspan-idabortauthspanabort-authentication"></a><span id="abortauth"></span><span id="ABORTAUTH"></span>中止身份验证


如果应用程序发现它无法生成当前的网络凭据 （漫游协议已更改，因为信息都是不可用，或由于其他原因），必须调用[ **AbortAuthentication**](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.HotspotAuthenticationContext#Windows_Networking_NetworkOperators_HotspotAuthenticationContext_AbortAuthentication_System_Boolean_)方法[ **HotspotAuthenticationContext** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.HotspotAuthenticationContext)对象。

Windows 从网络断开连接，并不会重新中当前用户会话的连接。 此函数接受一个标志，指示 Windows 应永远不会自动重试使用此配置文件的连接。

**请注意**  此方法不会从系统删除该配置文件和应用程序可以将要求提供凭据是否用户手动尝试连接到网络。 如果完全删除的配置文件，该应用程序必须提供删除关联的配置文件的新预配文件。

 

## <a name="span-idaltauthspanspan-idaltauthspanuse-alternate-authentication-methods"></a><span id="altauth"></span><span id="ALTAUTH"></span>使用备用身份验证方法


如果应用程序可以通过使用 WISPr 以外的方法进行身份验证，它可以这样做。 身份验证成功后到网络通过使用另一种方法，它必须在完成连接调用[ **SkipAuthentication** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.HotspotAuthenticationContext#Windows_Networking_NetworkOperators_HotspotAuthenticationContext_SkipAuthentication)方法[ **HotspotAuthenticationContext** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.HotspotAuthenticationContext)对象。 调用此方法时，Windows 将重新检测连接到 Internet，从而帮助用户界面 (UI) 以正确反映已经过身份验证的状态。

**请注意**   HotspotAuthentication 事件不为未公布 WISPr 协议支持的热点调用。 但是，这允许应用程序以选择要在响应中，使用不同协议或使用 WISPr 的自定义版本，如果所需。

 

## <a name="span-iduserintspanspan-iduserintspaninteract-with-the-user"></a><span id="userint"></span><span id="USERINT"></span>与用户交互


如果可以进行身份验证之前需要用户交互，该应用必须调用[ **TriggerAttentionRequired** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.HotspotAuthenticationContext#Windows_Networking_NetworkOperators_HotspotAuthenticationContext_TriggerAttentionRequired_System_String_System_String_)方法[ **HotspotAuthenticationContext** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.HotspotAuthenticationContext)对象。 此方法是在以下情况下有用：

-   用户已选择不在应用程序中存储凭据，并且必须登录。

-   完成该连接将收费，用户的信用卡或其他本地帐户。因此，继续下一步之前，必须同意的情况。

-   没有剩余信用位于用户的帐户，并且需要购买新。

此方法不会完成身份验证。 调用此方法时，应用将请求在前台打开通过使用指定的参数。 应将事件标记传递给前台应用程序，以便它可以检索[ **HotspotAuthenticationContext** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.HotspotAuthenticationContext)再次对象，并使用其他三个完成身份验证方法。

在前台打开应用的请求不能保证成功。 HotspotAuthentication 事件可能是因为自动连接计算机处于连接待机状态。 仅当计算机不再连接待机、 已解锁，又仍连接到无线网络时，启动应用程序。 因为这会延迟 Internet 访问权限，直到用户解锁计算机，可以自动生成的凭据时，应避免此状态。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[WISPr 身份验证](wispr-authentication.md)

 

 






