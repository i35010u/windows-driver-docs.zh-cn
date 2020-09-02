---
title: 移动宽带 Windows 运行时 API 的概述
description: 移动宽带 Windows 运行时 API 的概述
ms.assetid: 45ec97c4-1a58-48a8-ad50-1cd8fcc4763f
ms.date: 07/02/2019
ms.localizationpriority: medium
ms.openlocfilehash: d6efe7ae18896d7b5a11aed74020e9f476bde733
ms.sourcegitcommit: 7e4d9508198a30bdc1cb6eda83852dda4e42213e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89304262"
---
# <a name="overview-of-mobile-broadband-windows-runtime-apis"></a>移动宽带 Windows 运行时 API 的概述


下表列出了用于创作移动宽带应用程序的 Api。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>API</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="connection-profile-api.md" data-raw-source="[Connection Profile API](connection-profile-api.md)">连接配置文件 API</a></p></td>
<td><p>提供有关连接状态的信息 (例如，连接到 Internet) </p></td>
</tr>
<tr class="even">
<td><p><a href="device-services-extension-api.md" data-raw-source="[Device Services Extension API](device-services-extension-api.md)">设备服务扩展 API</a></p></td>
<td><p>启用设备特定的扩展，例如 SIM 工具包和首选漫游列表 (PRL) 下载。</p></td>
</tr>
<tr class="odd">
<td><p><a href="provisioning-api.md" data-raw-source="[Provisioning API](provisioning-api.md)">预配 API</a></p></td>
<td><p>使你能够使用帐户预配数据和数据使用信息来设置 Windows。</p></td>
</tr>
<tr class="even">
<td><p><a href="sim-pin-api.md" data-raw-source="[SIM PIN API](sim-pin-api.md)">SIM PIN API</a></p></td>
<td><p>使你能够启用、禁用或更改 SIM 卡 PIN。</p></td>
</tr>
<tr class="odd">
<td><p><a href="sms-api.md" data-raw-source="[SMS API](sms-api.md)">短信 API</a></p></td>
<td><p>提供实现 SMS 客户端所需的函数。</p></td>
</tr>
<tr class="even">
<td><p><a href="subscriber-and-device-information-api.md" data-raw-source="[Subscriber and Device Information API](subscriber-and-device-information-api.md)">订阅服务器和设备信息 API</a></p></td>
<td><p>提供移动宽带设备的 SIM 和设备信息的订阅者信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="ussd-api.md" data-raw-source="[USSD API](ussd-api.md)">USSD API</a></p></td>
<td><p>使你能够使用网络 (客户端和网络启动的) 建立 (USSD) 会话的非结构化补充服务数据。</p></td>
</tr>
</tbody>
</table>

 

本主题中提供了以下各节：

-   [移动宽带帐户 API](#mbacctapi)

-   [网络帐户 Id](#netid)

## <a name="span-idmbacctapispanspan-idmbacctapispanmobile-broadband-account-api"></a><span id="mbacctapi"></span><span id="MBACCTAPI"></span>移动宽带帐户 API


由于它有一些方法可用于获取有关客户的个人身份信息并在移动宽带设备上更改网络设置，因此移动宽带帐户 API 是一个特权 API。 这意味着大多数 UWP 应用无法调用其方法，且不会出现 "拒绝访问" 错误。 为了能够调用此 API，UWP 应用必须满足以下条件：

-   应用必须具有与之关联的设备元数据或服务元数据包，并且它必须在包中 SoftwareInfo.xml 文件的 [PrivilegedApplications](privilegedapplications.md) XML 元素中列出。 包不必对应用程序是唯一的;某些特定 UWP 应用可以在多个包的 PrivilegedApplications 元素中列出。 该程序包必须与在计算机上至少处于活动状态一次的移动宽带设备的服务提供商关联，使其已安装。

-   应用程序的 appxmanifest.xml 文件需要一个** &lt; DeviceCapability &gt; **条目用于移动宽带帐户 API。 为此，可以在应用程序的 appxmanifest.xml 文件中添加以下 XML 元素作为** &lt; 功能 &gt; **元素的子元素：

    ``` syntax
    <DeviceCapability Name="BFCD56F7-3943-457F-A312-2E19BB6DC648" />
    ```

    有关** &lt; 功能 &gt; **元素的详细信息，请参阅适用[于 Windows 8 的应用程序清单文件](/previous-versions/windows/apps/ff769509(v=vs.105))。

**注意**   不是 UWP 应用的应用程序 (例如，Microsoft Win32 服务或桌面应用) 可以无限制地访问移动宽带帐户 API。 这是因为，这些应用程序可以使用 (COM) Api 的现有 Win32 和组件对象模型来获取移动宽带网络的完全访问权限。 不能从 UWP 应用中使用这些 Api。

 

## <a name="span-idnetidspanspan-idnetidspannetwork-account-ids"></a><span id="netid"></span><span id="NETID"></span>网络帐户 Id


网络帐户 ID 是移动宽带帐户的唯一标识符。 它提供了一个统一 ID，无需知道 ID 是来自 GSM、CDMA 还是 WiMAX 网络即可使用。 每当 Windows 遇到之前尚未遇到的硬件提供的网络订阅标识符时，就会生成网络帐户 Id。 以下列表标识每个受支持的网络类型的网络帐户 ID：

-   GSM 网络： SIM 的 ICCID 用于区分订阅。

-   CDMA 网络：使用的移动标识号 (分钟) 。

如果 Windows 第一次遇到上述网络类型之一，则会创建新的网络帐户 ID，并将其映射到硬件提供的订阅标识符的 SHA-256 哈希，然后将它们存储在注册表中。 相反，如果 Windows 在注册表中找到硬件提供的订阅标识符的哈希，则它将使用与该哈希关联的网络帐户 ID。 网络帐户 Id 应全局唯一 (它们基于 Guid) ，但由于存储的是硬件提供的标识符的哈希，因此，在尝试将网络帐户 ID 映射回其生成的 ICCID 或最小值时，必须提供网络硬件。

**重要提示**   即使从网络帐户 ID 获取 ICCID 时，也需要访问计算机和网络设备（用于将它们映射到一起），网络帐户 Id 可以唯一地标识单个用户。 因此，我们建议您在使用组织的策略时，处理个人身份信息。

 

网络帐户 Id 通过移动网络操作员 (o) 隔离，因此，如果最终用户同时安装了 Provider1 和 Provider2 移动宽带设备，并安装了其相应的移动宽带应用，则 Provider1 应用将无法使用任何 Provider2 网络帐户 Id，反之亦然。 返回所有网络帐户 Id 的函数将仅返回其应用程序调用该函数的 o 的网络帐户 Id。 尝试使用属于不同 o 的网络帐户 ID 会导致 "拒绝访问" 错误。

**注意**   不是 UWP 应用 (例如，Win32 服务或桌面应用) 可以访问所有网络帐户，而无需考虑网络服务提供商。

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 WinRT API 概述](list-of-mobile-broadband-windows-runtime-apis.md)

 

