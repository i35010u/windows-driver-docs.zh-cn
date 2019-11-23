---
title: 设备对象的 SDDL
description: 设备对象的 SDDL
ms.assetid: c0e4432a-4429-4ecd-a2e5-f93a9e3caf48
keywords:
- 设备对象 WDK 内核，安全性
- 安全 WDK 设备对象
- 安全描述符定义语言 WDK 设备对象
- SDDL WDK 设备对象
- IoCreateDeviceSecure
- 安全描述符 WDK 设备对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c4a77cf0fb17fbbc5a8171ea050b034ba757fe4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836392"
---
# <a name="sddl-for-device-objects"></a>设备对象的 SDDL





安全描述符定义语言（SDDL）用于表示安全说明符。 设备对象的安全可以由[放置在 INF 文件中](https://docs.microsoft.com/windows-hardware/drivers/install/creating-secure-device-installations)或传递给[**IoCreateDeviceSecure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)的 SDDL 字符串指定。 [安全描述符定义语言](https://docs.microsoft.com/windows/desktop/SecAuthZ/security-descriptor-definition-language)完全记录在 Microsoft Windows SDK 文档中。

尽管 INF 文件支持全部 SDDL，但**IoCreateDeviceSecure**例程仅支持语言的子集。 此处定义了此子集。

设备对象的 SDDL 字符串的格式为 "D:P"，后跟一个或多个形式为 "（A;;*Access*;;;*SID*） "。 *SID*值指定一个安全标识符，该标识符确定*访问*值适用于的用户（例如，用户或组）。 *访问*值指定 SID 允许的访问权限。 *访问*和*SID*的值如下所示。

**请注意**，在对设备对象使用 SDDL 时  ，驱动程序必须针对 Wdmsec 进行链接。

 

<a href="" id="access"></a>*Access*  
指定用于确定允许的访问权限[ **\_掩码**](access-mask.md)值。 此值可以是以 "0x*hex*" 形式表示的十六进制值，也可以是表示访问权限的由两个字母构成的符号代码组成的序列。

以下代码可用于指定一般访问权限。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>代码</th>
<th>一般访问权限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>GA</p></td>
<td><p>GENERIC_ALL</p></td>
</tr>
<tr class="even">
<td><p>GR</p></td>
<td><p>GENERIC_READ</p></td>
</tr>
<tr class="odd">
<td><p>GW</p></td>
<td><p>GENERIC_WRITE</p></td>
</tr>
<tr class="even">
<td><p>GX</p></td>
<td><p>GENERIC_EXECUTE</p></td>
</tr>
</tbody>
</table>

 

可以使用以下代码指定特定访问权限。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>代码</th>
<th>特定访问权限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>.RC</p></td>
<td><p>READ_CONTROL</p></td>
</tr>
<tr class="even">
<td><p>SD</p></td>
<td><p>DELETE</p></td>
</tr>
<tr class="odd">
<td><p>WD</p></td>
<td><p>WRITE_DAC</p></td>
</tr>
<tr class="even">
<td><p>WO</p></td>
<td><p>WRITE_OWNER</p></td>
</tr>
</tbody>
</table>

 

请注意，一般\_都授予上述两个表中列出的所有权限，包括更改 ACL 的能力。

<a href="" id="sid"></a>*SID*  
指定授予指定访问权限的 SID。 Sid 表示帐户、别名、组、用户或计算机。

以下 Sid 表示计算机上的*帐户*。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>SID</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SY</p></td>
<td><p>系统</p>
<p>表示操作系统本身，其中包括其用户模式组件。</p></td>
</tr>
<tr class="even">
<td><p>'</p></td>
<td><p>本地服务</p>
<p>本地服务的预定义帐户（也属于已经过身份验证和世界）。 从 Windows XP 开始可以使用此 SID。</p></td>
</tr>
<tr class="odd">
<td><p>N</p></td>
<td><p>Network Service (网络服务)</p>
<p>用于网络服务的预定义帐户（也属于已经过身份验证和世界）。 从 Windows XP 开始可以使用此 SID。</p></td>
</tr>
</tbody>
</table>

 

以下 Sid 代表计算机上的*组*。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>SID</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>BA</p></td>
<td><p>Administrators</p>
<p>计算机上的内置 Administrators 组。</p></td>
</tr>
<tr class="even">
<td><p>BU</p></td>
<td><p>内置用户组</p>
<p>涵盖所有本地用户帐户和域中的用户的组。</p></td>
</tr>
<tr class="odd">
<td><p>BG</p></td>
<td><p>内置来宾组</p>
<p>涵盖使用本地或域来宾帐户登录的用户的组。</p></td>
</tr>
</tbody>
</table>

 

以下 Sid 描述了用户已进行身份验证的范围。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>SID</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AU</p></td>
<td><p>经过身份验证的用户</p>
<p>本地计算机或域识别的任何用户。 请注意，使用内置来宾帐户登录的用户不会进行身份验证。 但是，在计算机或域中具有个人帐户的来宾组的成员将进行身份验证。</p></td>
</tr>
<tr class="even">
<td><p>无</p></td>
<td><p>匿名登录的用户</p>
<p>任何未使用标识登录的用户，例如匿名网络会话。 请注意，使用内置来宾帐户登录的用户既不进行身份验证，也不是匿名的。 从 Windows XP 开始可以使用此 SID。</p></td>
</tr>
</tbody>
</table>

 

以下 Sid 说明用户如何登录到计算机。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>SID</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IU</p></td>
<td><p>交互式用户</p>
<p>最初以交互方式登录到计算机的用户，例如本地登录和远程桌面登录。</p></td>
</tr>
<tr class="even">
<td><p>NU</p></td>
<td><p>网络登录用户</p>
<p>远程访问计算机，无需交互式桌面访问（例如，文件共享或 RPC 调用）的用户。</p></td>
</tr>
<tr class="odd">
<td><p>WD</p></td>
<td><p>World</p>
<p>在 Windows XP 之前，此 SID 涵盖每个会话，无论是经过身份验证的用户、匿名用户还是内置来宾帐户。</p>
<p>从 Windows XP 开始，此 SID 不涵盖匿名登录会话;它仅包括经过身份验证的用户和内置来宾帐户。</p>
<p>请注意，世界 SID 还不包含不受信任或 "受限" 的代码。 有关详细信息，请参阅下表中的限制代码（RC） SID 的说明。</p></td>
</tr>
</tbody>
</table>

 

以下 Sid 值得特别指出。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>SID</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>.RC</p></td>
<td><p>限制代码</p>
<p>此 SID 用于控制不受信任的代码的访问。 针对带有 RC 的令牌的 ACL 验证包括两个检查，一个针对令牌的正常 Sid 列表（包含 WD），另一个针对第二个列表（通常包含 RC 和原始令牌 Sid 的子集）。 仅当令牌同时通过这两个测试时，才授予访问权限。 因此，RC 实际上与其他 Sid 一起工作。</p>
<p>指定 RC 的任何 ACL 还必须指定 WD。 当 RC 与 ACL 中的 WD 配对时，将描述包含不受信任代码的所有用户的超集。</p>
<p>不受信任的代码可能是使用资源管理器中的 "运行方式" 选项启动的代码。 默认情况下，World 不涵盖不受信任的代码。</p></td>
</tr>
<tr class="even">
<td><p>UD</p></td>
<td><p>用户模式驱动程序</p>
<p>此 SID 授予对用户模式驱动程序的访问权限。 目前，此 SID 只包含为用户模式驱动程序框架（UMDF）编写的驱动程序。 从 Windows 8 开始可以使用此 SID。</p>
<p>在早期版本的 Windows 中，如果不能识别 "UD" 缩写，则必须指定此 SID 的完全限定形式（S-1-5-84-0-0-0-0-0），以授予对 UMDF 驱动程序的访问权限。 有关详细信息，请参阅在用户模式驱动程序框架中<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/controlling-device-access" data-raw-source="[Controlling Device Access](https://docs.microsoft.com/windows-hardware/drivers/wdf/controlling-device-access)">控制设备访问</a>文档。</p></td>
</tr>
</tbody>
</table>

 

### <a name="sddl-examples-for-device-objects"></a>设备对象的 SDDL 示例

本部分介绍在 Wdmsec 中找到的预定义 SDDL 字符串。 你还可以使用这些模板来定义设备对象的新 SDDL 字符串。

SDDL\_DEVOBJ\_仅限内核\_

**"D:P"**

SDDL\_DEVOBJ\_内核\_只是 "空" 的 ACL。 用户模式代码（包括作为系统运行的进程）无法打开该设备。

在创建 PDO 时，PnP 总线驱动程序可以使用此描述符。 INF 文件随后可以指定设备的更松散安全设置。 通过指定此描述符，总线驱动程序将确保在处理 INF 之前，不会尝试打开设备。

同样，非 WDM 驱动程序可以使用此描述符使其设备对象不可访问，直到适当的用户模式程序（如安装程序）设置注册表中的最终安全描述符。

在所有这些情况下，默认值都是严格的安全性，必要时放松。

SDDL\_DEVOBJ\_SYS\_全部

**"D:P （A;;GA;;;SY） "**

SDDL\_DEVOBJ\_SYS\_全部与 SDDL\_DEVOBJ\_内核\_类似，除了内核模式代码外，还允许作为系统运行的用户模式代码打开设备进行任何访问。

旧的驱动程序可能使用此 ACL 以严格的安全设置开始，并使其服务在运行时使用**SetFileSecurity**用户模式功能将设备打开到各个用户。 在这种情况下，服务必须作为系统运行。

SDDL\_DEVOBJ\_SYS\_所有\_ADM\_

**"D:P （A;;GA;;;SY）（A;;GA;;;BA） "**

SDDL\_DEVOBJ\_SYS\_所有\_ADM\_全部允许内核、系统和管理员完全控制设备。 其他用户无法访问设备。

SDDL\_DEVOBJ\_SYS\_所有\_ADM\_RWX\_WORLD\_

**"D:P （A;;GA;;;SY）（A;;GRGWGX;;;BA）（A;;GR;;;WD） "**

SDDL\_DEVOBJ\_SYS\_所有\_ADM\_RWX\_WORLD\_R 允许内核和系统完全控制设备。 默认情况下，管理员可以访问整个设备，但不能更改 ACL （管理员必须先控制设备。）

为每个人（世界 SID）提供读取访问权限。 不受信任的代码不能访问该设备（不受信任的代码可能是使用资源管理器中的运行方式选项启动的代码。 默认情况下，World 不包含受限制的代码。）

另请注意，不会向普通用户授予遍历访问权限。 因此，对于具有命名空间的设备，这可能不是合适的描述符。

SDDL\_DEVOBJ\_SYS\_所有\_ADM\_RWX\_WORLD\_R\_\_

**"D:P （A;;GA;;;SY）（A;;GRGWGX;;;BA）（A;;GR;;;WD）（A;;GR;;;RC） "**

SDDL\_DEVOBJ\_SYS\_所有\_ADM\_RWX\_世界\_R\_RES\_R 允许内核和系统完全控制设备。 默认情况下，管理员可以访问整个设备，但不能更改 ACL （管理员必须先控制设备。）

为每个人（世界 SID）提供读取访问权限。 此外，还允许不受信任的代码访问代码。 不受信任的代码可能是使用资源管理器中的 "运行方式" 选项启动的代码。 默认情况下，World 不包含受限制的代码。

另请注意，不会向普通用户授予遍历访问权限。 因此，对于具有命名空间的设备，这可能不是合适的描述符。

 

请注意，上述 SDDL 字符串不包含任何继承修饰符。 因此，它们仅适用于设备对象，不应用于文件或注册表项。 有关使用 SDDL 指定继承的详细信息，请参阅 Microsoft Windows SDK 文档。

 

 




