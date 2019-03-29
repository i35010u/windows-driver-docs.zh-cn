---
title: 设备对象的 SDDL
description: 设备对象的 SDDL
ms.assetid: c0e4432a-4429-4ecd-a2e5-f93a9e3caf48
keywords:
- 设备对象 WDK 内核安全性
- 安全 WDK 设备对象
- 安全描述符定义语言 WDK 设备对象
- SDDL WDK 设备对象
- IoCreateDeviceSecure
- 安全描述符 WDK 设备对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 223c6ae8277ad5a31984ecdf1c3ada1851b941b3
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464345"
---
# <a name="sddl-for-device-objects"></a>设备对象的 SDDL





安全描述符定义语言 (SDDL) 用于表示安全描述符。 是一个 SDDL 字符串可以指定设备对象的安全[INF 文件中放置](https://msdn.microsoft.com/library/windows/hardware/ff540212)或传递给[ **IoCreateDeviceSecure**](https://msdn.microsoft.com/library/windows/hardware/ff548407)。 [安全描述符定义语言](https://msdn.microsoft.com/library/windows/desktop/aa379567)完全记录在 Microsoft Windows SDK 文档。

虽然 INF 文件支持完整范围的 SDDL，但通过支持语言的一个子集**IoCreateDeviceSecure**例程。 在此处定义该子集。

SDDL 字符串的设备对象的窗体"D:P"后面跟有一个或多个表达式的窗体"(A;*访问*;;*SID*)"。 *SID*值指定安全标识符，用于确定向其*访问*值将应用 （适用于示例中，用户或组）。 *访问*值指定允许的 sid 的访问权限。 *访问*并*SID*值如下所示。

**请注意**  时使用的设备对象的 SDDL，针对 Wdmsec.lib 必须链接您的驱动程序。

 

<a href="" id="access"></a>*Access*  
指定[**访问权限\_掩码**](access-mask.md)值，该值确定允许的访问。 此值可以为十六进制值形式编写的"0x*十六进制*"，或为一系列的两个字母的符号代码表示的访问权限。

以下代码可用于指定通用访问权限。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>代码</th>
<th>通用访问权限</th>
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

 

以下代码可用于指定特定访问权限。

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

 

请注意该泛型\_上述两个表，包括能够更改 ACL 中列出的所有授予所有权限。

<a href="" id="sid"></a>*SID*  
指定授予指定的访问权限的 SID。 表示 Sid 的帐户、 别名、 组、 用户或计算机。

以下 Sid 代表*帐户*在计算机上。

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
<p>表示操作系统本身，包括其用户模式组件。</p></td>
</tr>
<tr class="even">
<td><p>LS</p></td>
<td><p>本地服务</p>
<p>预定义的帐户为本地服务的 （这同时也属于已经过身份验证和 World）。 此 SID 是从 Windows XP 开始提供。</p></td>
</tr>
<tr class="odd">
<td><p>NS</p></td>
<td><p>Network Service (网络服务)</p>
<p>用于网络服务的预定义的帐户 （这同时也属于已经过身份验证和 World）。 此 SID 是从 Windows XP 开始提供。</p></td>
</tr>
</tbody>
</table>

 

以下 Sid 代表*组*在计算机上。

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
<p>在计算机上内置管理员组。</p></td>
</tr>
<tr class="even">
<td><p>BU</p></td>
<td><p>内置用户组</p>
<p>介绍了所有本地用户帐户和域上的用户组。</p></td>
</tr>
<tr class="odd">
<td><p>BG</p></td>
<td><p>内置来宾组</p>
<p>介绍在使用本地或域来宾帐户登录的用户组。</p></td>
</tr>
</tbody>
</table>

 

以下 Sid 描述向其验证用户的范围。

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
<td><p>身份验证的用户</p>
<p>由本地计算机或域识别的任何用户。 请注意，使用内置来宾帐户登录的用户未经过身份验证。 但是，使用单个帐户在计算机或域上的来宾组的成员进行身份验证。</p></td>
</tr>
<tr class="even">
<td><p>AN</p></td>
<td><p>匿名登录的用户</p>
<p>任何用户，而无需标识，如匿名网络会话登录。 请注意，在使用内置来宾帐户登录的用户既没有经过身份验证，也没有匿名。 此 SID 是从 Windows XP 开始提供。</p></td>
</tr>
</tbody>
</table>

 

以下 Sid 介绍用户如何登录到计算机。

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
<td><p>交互用户</p>
<p>最初登录到计算机"以交互方式"，如本地登录和远程桌面登录的用户。</p></td>
</tr>
<tr class="even">
<td><p>NU</p></td>
<td><p>网络登录用户</p>
<p>远程访问计算机，而不会 （例如，文件共享或 RPC 调用） 的交互式桌面访问权限的用户。</p></td>
</tr>
<tr class="odd">
<td><p>WD</p></td>
<td><p>World</p>
<p>在 Windows XP 之前此 SID 涵盖每个会话是否经过身份验证的用户、 匿名用户或内置来宾帐户。</p>
<p>从 Windows XP 开始，此 SID 不涉及匿名登录会话;它介绍了只有经过身份验证的用户和内置来宾帐户。</p>
<p>请注意不受信任或"受限"代码也不涵盖了世界 SID。 有关详细信息，请参阅下表中的说明的受限代码 (RC) 的 SID。</p></td>
</tr>
</tbody>
</table>

 

以下 Sid 值得注意。

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
<td><p>受限制的代码</p>
<p>此 SID 用于受信任的代码控制访问权限。 对 rc 的令牌进行 ACL 验证由两个检查，一个针对 Sid （例如包含 WD），该令牌的正常列表，一个根据第二个列表 （通常包含 RC 和原始令牌 Sid 的子集） 组成。 如果一个令牌将传递两个测试仅授予访问权限。 在这种情况下，RC 实际上结合使用其他的 Sid。</p>
<p>指定 RC 任何 ACL 还必须指定 WD。 时与 ACL 中 WD 配对 RC，描述了每个人都包括不受信任的代码的超集。</p>
<p>不受信任的代码可能是在资源管理器中使用运行方式选项启动的代码。 默认情况下，世界不涉及不受信任的代码。</p></td>
</tr>
<tr class="even">
<td><p>UD</p></td>
<td><p>用户模式驱动程序</p>
<p>此 SID 授予访问权限的用户模式驱动程序。 目前，此 SID 包含仅专为用户模式驱动程序框架 (UMDF) 的驱动程序。 此 SID 是从 Windows 8 开始提供。</p>
<p>在早期版本的 Windows，不能识别"UD"缩写，必须指定完全限定的窗体的此 SID (S-1-5-84-0-0-0-0-0) 授予对 UMDF 驱动程序访问权限。 有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/hh439567" data-raw-source="[Controlling Device Access](https://msdn.microsoft.com/library/windows/hardware/hh439567)">控制的设备访问</a>用户模式驱动程序框架文档中。</p></td>
</tr>
</tbody>
</table>

 

### <a name="sddl-examples-for-device-objects"></a>设备对象的 SDDL 示例

本部分介绍在 Wdmsec.h 中找到的预定义的 SDDL 字符串。 此外可以使用这些作为模板来定义新的设备对象的 SDDL 字符串。

SDDL\_DEVOBJ\_KERNEL\_ONLY

**"D:P"**

SDDL\_DEVOBJ\_内核\_只是"空"的 ACL。 用户模式代码 （包括作为系统运行的进程） 无法打开设备。

创建一个 PDO 时，即插即用总线驱动程序无法使用此说明符。 INF 文件然后可以指定更松散的设备的安全设置。 通过指定此说明符，总线驱动程序将确保不会尝试打开设备 INF 已处理之前会成功。

同样，非 WDM 驱动程序可以使用此说明符以使其设备对象不可访问，直到相应用户模式 （例如安装程序） 的程序在注册表中设置的最后一个安全描述符。

在所有这些情况下，默认值是严格的安全措施，根据需要放松。

SDDL\_DEVOBJ\_SYS\_ALL

**"D:P(A;;GA;;;SY)"**

SDDL\_DEVOBJ\_SYS\_就是类似于 SDDL\_DEVOBJ\_内核\_仅，不同之处在于除了内核模式代码，用户模式下作为系统运行还允许代码打开设备的任何访问。

旧驱动程序可能会使用此 ACL 以启动带严谨的安全设置，并让打开设备在运行时对单个用户使用其服务**SetFileSecurity**用户模式下函数。 在这种情况下，该服务必须以系统帐户运行。

SDDL\_DEVOBJ\_SYS\_ALL\_ADM\_ALL

**"D:P(A;;GA;;;SY)(A;;GA;;;BA)"**

SDDL\_DEVOBJ\_SYS\_所有\_ADM\_所有允许对设备内核、 系统和管理员的完全控制。 其他用户不可能访问该设备。

SDDL\_DEVOBJ\_SYS\_ALL\_ADM\_RWX\_WORLD\_R

**"D:P(A;;GA;;;SY)(A;;GRGWGX;;;BA)(A;;GR;;;WD)"**

SDDL\_DEVOBJ\_SYS\_所有\_ADM\_RWX\_世界\_R 允许设备对内核和系统的完全控制。 默认情况下，管理员可以访问整个设备，但不能更改的 ACL （管理员必须采取对设备的控制第一次。）

每个人 (世界 SID) 是授予读取访问权限。 不受信任的代码无法访问设备 （不受信任的代码可能是代码资源管理器中使用运行方式选项启动。 默认情况下，世界不涉及受限制的代码。）

另请注意，普通用户不允许遍历访问。 在这种情况下，这可能不是适当的描述符具有命名空间的设备。

SDDL\_DEVOBJ\_SYS\_ALL\_ADM\_RWX\_WORLD\_R\_RES\_R

**"D:P(A;;GA;;;SY)(A;;GRGWGX;;;BA)(A;;GR;;;WD)(A;;GR;;;RC)"**

SDDL\_DEVOBJ\_SYS\_所有\_ADM\_RWX\_世界\_R\_RES\_R 允许设备对内核和系统的完全控制。 默认情况下，管理员可以访问整个设备，但不能更改的 ACL （管理员必须采取对设备的控制第一次。）

每个人 (世界 SID) 是授予读取访问权限。 此外，不受信任的代码还允许的访问代码。 不受信任的代码可能是在资源管理器中使用运行方式选项启动的代码。 默认情况下，世界不涉及受限制的代码。

另请注意，普通用户不允许遍历访问。 在这种情况下，这可能不是适当的描述符具有命名空间的设备。

 

请注意，上面的 SDDL 字符串不包括任何继承修饰符。 在这种情况下，它们了仅适用于设备对象，因此不应为文件或注册表项。 有关指定使用 SDDL 继承的详细信息，请参阅 Microsoft Windows SDK 文档。

 

 




