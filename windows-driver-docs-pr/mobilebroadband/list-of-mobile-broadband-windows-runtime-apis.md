---
title: 移动宽带 Windows 运行时 API 的列表
description: 移动宽带 Windows 运行时 API 的列表
ms.assetid: 45ec97c4-1a58-48a8-ad50-1cd8fcc4763f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 561d6c1eabda02ac372a62d083f855c7100ccdab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380377"
---
# <a name="list-of-mobile-broadband-windows-runtime-apis"></a>移动宽带 Windows 运行时 API 的列表


下表列出了用于创作移动宽带应用的 Api。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>API</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="connection-profile-api.md" data-raw-source="[Connection Profile API](connection-profile-api.md)">连接配置文件 API</a></p></td>
<td><p>提供有关连接状态的信息 （例如，对 Internet)</p></td>
</tr>
<tr class="even">
<td><p><a href="device-services-extension-api.md" data-raw-source="[Device Services Extension API](device-services-extension-api.md)">设备服务扩展 API</a></p></td>
<td><p>启用特定于设备的扩展，例如 SIM 工具包和首选漫游列表 (PRL) 下载。</p></td>
</tr>
<tr class="odd">
<td><p><a href="provisioning-api.md" data-raw-source="[Provisioning API](provisioning-api.md)">预配 API</a></p></td>
<td><p>可以预配 Windows 帐户预配数据和数据使用情况信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="sim-pin-api.md" data-raw-source="[SIM PIN API](sim-pin-api.md)">SIM 卡 PIN API</a></p></td>
<td><p>可以启用、 禁用或更改 SIM PIN。</p></td>
</tr>
<tr class="odd">
<td><p><a href="sms-api.md" data-raw-source="[SMS API](sms-api.md)">SMS API</a></p></td>
<td><p>提供了实现 SMS 客户端所需的函数。</p></td>
</tr>
<tr class="even">
<td><p><a href="subscriber-and-device-information-api.md" data-raw-source="[Subscriber and Device Information API](subscriber-and-device-information-api.md)">订阅服务器和设备信息 API</a></p></td>
<td><p>提供移动宽带设备的 SIM 和设备信息的订阅者信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="ussd-api.md" data-raw-source="[USSD API](ussd-api.md)">USSD API</a></p></td>
<td><p>使您能够建立与网络 （客户端和网络启动） 的非结构化补充服务数据 (USSD) 会话。</p></td>
</tr>
</tbody>
</table>

 

本主题中提供了以下各节：

-   [移动宽带帐户 API](#mbacctapi)

-   [网络帐户 Id](#netid)

## <a name="span-idmbacctapispanspan-idmbacctapispanmobile-broadband-account-api"></a><span id="mbacctapi"></span><span id="MBACCTAPI"></span>移动宽带帐户 API


因为它具有可以用于获取有关客户的个人身份信息和更改移动宽带设备上的网络设置的方法，移动宽带帐户 API 是一个特权的 API。 这意味着大多数 UWP 应用不能调用其方法而不会获得"拒绝访问"错误。 若要能够调用此 API，UWP 应用必须满足以下条件：

-   应用必须具有与之关联，设备元数据或服务元数据包和必须以列出[PrivilegedApplications](privilegedapplications.md) SoftwareInfo.xml 文件在包内的 XML 元素。 包没有为专用于该应用程序;就可以为任何特定的 UWP 应用以多个包的 PrivilegedApplications 元素中列出。 该包必须与保持活动状态的至少一次在计算机的移动宽带设备的服务提供程序相关联，以便已安装。

-   应用程序的 appxmanifest 文件需要 **&lt;DeviceCapability&gt;** 条目移动宽带帐户 API。 您可以执行此操作通过将下面的 XML 元素添加为的子 **&lt;功能&gt;** 应用程序的 appxmanifest 文件中的元素：

    ``` syntax
    <DeviceCapability Name="BFCD56F7-3943-457F-A312-2E19BB6DC648" />
    ```

    有关详细信息 **&lt;功能&gt;** 元素中，请参阅[应用程序清单文件适用于 Windows 8 的](https://msdn.microsoft.com/library/windows/apps/ff769509.aspx)。

**请注意**  不 UWP 应用 （例如，Microsoft Win32 服务或桌面应用程序） 的应用程序可以无限制地访问移动宽带帐户 API。 这是因为这些应用程序可以使用现有 Win32 和组件对象模型 (COM) Api 获取到移动宽带网络的完全访问权限。 不能从 UWP 应用使用这些 Api。

 

## <a name="span-idnetidspanspan-idnetidspannetwork-account-ids"></a><span id="netid"></span><span id="NETID"></span>网络帐户 Id


网络帐户 ID 是移动宽带帐户的唯一标识符。 它提供了一个统一的 ID，可以使用而无需知道是否 ID 来自 GSM、 CDMA 或 WiMAX 网络。 遇到它以前未遇到过的硬件提供网络订阅标识符时，Windows 将生成网络帐户 Id。 以下列表标识了每种支持的网络类型的网络帐户 ID:

-   GSM 网络：SIM ICCID 用于区分订阅。

-   CDMA 网络：使用移动标识号 （分钟）。

当 Windows 遇到一个前面的网络类型的第一次时，它将创建一个新的网络帐户 ID 和将其映射到的硬件提供的订阅标识符，SHA-256 哈希，然后将这两个值存储在注册表中。 相反，如果 Windows 注册表中发现的硬件提供的订阅标识符的哈希，它使用与该哈希相关联的网络帐户 ID。 网络帐户 Id 应是全局唯一 （它们基于 Guid），但存储的内容是提供硬件标识符的哈希，因为网络硬件必须存在时尝试映射回的 ICCID 或它所生成的最小的网络帐户 ID从。

**重要**  即使从网络帐户 ID 获取 ICCID 需要访问计算机和用于映射在一起的网络设备，网络 Id 唯一地标识单个用户帐户。 因此，我们建议您正在使用它们时请遵循处理个人身份信息的组织的策略。

 

网络帐户 Id 是按移动网络运营商 (MNO) 隔离，因此，如果最终用户有 Provider1 和 Provider2 移动宽带设备，且其相应的移动宽带应用程序安装，Provider1 应用将不能使用任何 Provider2网络帐户 Id，反之亦然。 返回所有网络帐户 Id 将都返回仅的网络帐户 Id m n O 其应用程序的函数调用该函数。 尝试使用属于不同 m n O 的网络帐户 ID 将导致"拒绝访问"错误。

**请注意**  不 UWP 应用 （例如，Win32 服务或桌面应用程序） 的应用有权访问所有的网络帐户，而不考虑网络服务提供商。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带的 WinRT API 概述](mobile-broadband-winrt-api-overview.md)

 

 






