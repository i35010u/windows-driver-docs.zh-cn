---
title: 设备对象的 SDDL
description: 设备对象的 SDDL
keywords:
- 设备对象 WDK 内核，安全性
- 安全 WDK 设备对象
- 安全描述符定义语言 WDK 设备对象
- SDDL WDK 设备对象
- IoCreateDeviceSecure
- 安全描述符 WDK 设备对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41089b35c4555e2b930fca067c03ccc57fefc5ae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823963"
---
# <a name="sddl-for-device-objects"></a>设备对象的 SDDL





安全描述符定义语言 (SDDL) 用于表示安全描述符。 设备对象的安全可以由 [放置在 INF 文件中](../install/creating-secure-device-installations.md) 或传递给 [**IoCreateDeviceSecure**](/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)的 SDDL 字符串指定。 [安全描述符定义语言](/windows/desktop/SecAuthZ/security-descriptor-definition-language)完全记录在 Microsoft Windows SDK 文档中。

尽管 INF 文件支持全部 SDDL，但 **IoCreateDeviceSecure** 例程仅支持语言的子集。 此处定义了此子集。

设备对象的 SDDL 字符串的格式为 "D:P"，后跟一个或多个 " (;" 形式的表达式。*Access*;;;*SID*) "。 *SID* 值指定一个安全标识符，该标识符确定 *访问* 值适用的目标 (例如，用户或组) 。 *访问* 值指定 SID 允许的访问权限。 *访问* 和 *SID* 的值如下所示。

**注意**  使用 SDDL 作为设备对象时，驱动程序必须针对 Wdmsec 进行链接。

 

<a href="" id="access"></a>*Access*  
指定用于确定允许的访问权限的 [**访问 \_ 掩码**](access-mask.md) 值。 此值可以是以 "0x *hex*" 形式表示的十六进制值，也可以是表示访问权限的由两个字母构成的符号代码组成的序列。

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
<td><p>RC</p></td>
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

 

请注意，一般 \_ 所有权限都授予上述两个表中列出的所有权限，包括更改 ACL 的能力。

<a href="" id="sid"></a>*SID*  
指定授予指定访问权限的 SID。 Sid 表示帐户、别名、组、用户或计算机。

以下 Sid 表示计算机上的 *帐户* 。

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
<td><p>LS</p></td>
<td><p>Local Service</p>
<p>本地服务 (的预定义帐户，该帐户也属于已经过身份验证和世界) 。 从 Windows XP 开始可以使用此 SID。</p></td>
</tr>
<tr class="odd">
<td><p>NS</p></td>
<td><p>Network Service</p>
<p>网络服务 (的预定义帐户，也属于经过身份验证和世界) 。 从 Windows XP 开始可以使用此 SID。</p></td>
</tr>
</tbody>
</table>

 

以下 Sid 代表计算机上的 *组* 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>SID</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>BA</p></td>
<td><p>管理员</p>
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
<td><p>AN</p></td>
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
<p>远程访问计算机的用户无需交互式桌面访问 (例如，) 的文件共享或 RPC 调用。</p></td>
</tr>
<tr class="odd">
<td><p>WD</p></td>
<td><p>World</p>
<p>在 Windows XP 之前，此 SID 涵盖每个会话，无论是经过身份验证的用户、匿名用户还是内置来宾帐户。</p>
<p>从 Windows XP 开始，此 SID 不涵盖匿名登录会话;它仅包括经过身份验证的用户和内置来宾帐户。</p>
<p>请注意，世界 SID 还不包含不受信任或 "受限" 的代码。 有关详细信息，请参阅下表中 (RC) SID 的受限制代码的说明。</p></td>
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
<td><p>RC</p></td>
<td><p>限制代码</p>
<p>此 SID 用于控制不受信任的代码的访问。 针对具有 RC 的令牌的 ACL 验证包含两个检查，一个针对令牌的正常 Sid 列表 (包含实例) 的 WD，另一个针对第二个列表 (通常包含 RC 和原始令牌 Sid) 的子集。 仅当令牌同时通过这两个测试时，才授予访问权限。 因此，RC 实际上与其他 Sid 一起工作。</p>
<p>指定 RC 的任何 ACL 还必须指定 WD。 当 RC 与 ACL 中的 WD 配对时，将描述包含不受信任代码的所有用户的超集。</p>
<p>不受信任的代码可能是使用资源管理器中的 "运行方式" 选项启动的代码。 默认情况下，World 不涵盖不受信任的代码。</p></td>
</tr>
<tr class="even">
<td><p>UD</p></td>
<td><p>User-Mode 驱动程序</p>
<p>此 SID 授予对用户模式驱动程序的访问权限。 目前，此 SID 只包含为 User-Mode Driver Framework 编写的驱动程序 (UMDF) 。 从 Windows 8 开始可以使用此 SID。</p>
<p>在早期版本的 Windows 中，如果不能识别 "UD" 缩写，则必须指定该 SID 的完全限定形式 (S-1-5-84-0-0-0-0-0) ，才能授予对 UMDF 驱动程序的访问权限。 有关详细信息，请参阅 User-Mode Driver Framework 文档中的 <a href="/windows-hardware/drivers/wdf/controlling-device-access" data-raw-source="[Controlling Device Access](../wdf/controlling-device-access.md)">控制设备访问权限</a> 。</p></td>
</tr>
</tbody>
</table>

 

### <a name="sddl-examples-for-device-objects"></a>设备对象的 SDDL 示例

本部分介绍在 Wdmsec 中找到的预定义 SDDL 字符串。 你还可以使用这些模板来定义设备对象的新 SDDL 字符串。

SDDL \_ DEVOBJ \_ \_ 仅内核

**"D:P"**

SDDL \_ DEVOBJ \_ 内核 \_ 仅为 "空" ACL。 用户模式代码 (包括作为系统运行的进程) 无法打开设备。

在创建 PDO 时，PnP 总线驱动程序可以使用此描述符。 INF 文件随后可以指定设备的更松散安全设置。 通过指定此描述符，总线驱动程序将确保在处理 INF 之前，不会尝试打开设备。

同样，非 WDM 驱动程序可以使用此描述符使其设备对象不可访问，直到在适当的用户模式程序 (如安装程序) 在注册表中设置最终安全描述符。

在所有这些情况下，默认值都是严格的安全性，必要时放松。

SDDL \_ DEVOBJ \_ SYS \_ ALL

**"D:P (A;;GA;;;SY) "**

SDDL \_ DEVOBJ \_ SYS \_ ALL 仅与 SDDL \_ DEVOBJ \_ 内核相似 \_ ，不同之处在于除了内核模式代码外，还允许作为系统运行的用户模式代码打开设备以进行任何访问。

旧的驱动程序可能使用此 ACL 以严格的安全设置开始，并使其服务在运行时使用 **SetFileSecurity** 用户模式功能将设备打开到各个用户。 在这种情况下，服务必须作为系统运行。

SDDL \_ DEVOBJ \_ SYS \_ ALL 所有 \_ ADM \_

**"D:P (A;;GA;;;SY) # B2 A;;GA;;;BA) "**

SDDL \_ DEVOBJ \_ SYS \_ all \_ ADM 全部 \_ 允许内核、系统和管理员对设备进行完全控制。 其他用户无法访问设备。

SDDL \_ DEVOBJ \_ SYS \_ ALL \_ ADM \_ RWX \_ WORLD \_ R

**"D:P (A;;GA;;;SY) # B2 A;;GRGWGX;;;BA) # B4 A;;GR;;;WD) "**

SDDL \_ DEVOBJ \_ SYS \_ ALL \_ ADM \_ RWX \_ WORLD \_ R 允许内核和系统完全控制设备。 默认情况下，管理员可以访问整个设备，但不能更改 ACL (管理员必须先控制设备。 ) 

将为世界 SID)  (的所有人提供读取访问权限。 不受信任的代码无法访问设备 (不受信任的代码可能是使用资源管理器中的 "运行方式" 选项启动的代码。 默认情况下，World 不会涵盖受限制的代码。 ) 

另请注意，不会向普通用户授予遍历访问权限。 因此，对于具有命名空间的设备，这可能不是合适的描述符。

SDDL \_ DEVOBJ \_ SYS \_ ALL \_ ADM \_ RWX \_ WORLD \_ R \_ RES \_ R

**"D:P (A;;GA;;;SY) # B2 A;;GRGWGX;;;BA) # B4 A;;GR;;;WD) # B6 A;;GR;;;RC) "**

SDDL \_ DEVOBJ \_ SYS \_ ALL \_ ADM \_ RWX \_ WORLD \_ r \_ RES \_ r 允许内核和系统完全控制设备。 默认情况下，管理员可以访问整个设备，但不能更改 ACL (管理员必须先控制设备。 ) 

将为世界 SID)  (的所有人提供读取访问权限。 此外，还允许不受信任的代码访问代码。 不受信任的代码可能是使用资源管理器中的 "运行方式" 选项启动的代码。 默认情况下，World 不包含受限制的代码。

另请注意，不会向普通用户授予遍历访问权限。 因此，对于具有命名空间的设备，这可能不是合适的描述符。

 

请注意，上述 SDDL 字符串不包含任何继承修饰符。 因此，它们仅适用于设备对象，不应用于文件或注册表项。 有关使用 SDDL 指定继承的详细信息，请参阅 Microsoft Windows SDK 文档。

