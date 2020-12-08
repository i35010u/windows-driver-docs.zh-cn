---
title: 显示驱动程序的版本号
description: 显示驱动程序的版本号
keywords:
- 版本号 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a521d66a09127b2b9ea062266ee6826383e388dc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798255"
---
# <a name="version-numbers-for-display-drivers"></a>显示驱动程序的版本号


## <span id="ddk_ensuring_correct_version_numbers_gg"></span><span id="DDK_ENSURING_CORRECT_VERSION_NUMBERS_GG"></span>


若要确保最终用户能够在特定操作系统上使用显示器驱动程序并使用特定版本的 DirectX，则必须将相应的版本号应用于该驱动程序。 使用 DirectX 时，版本号对于设备驱动程序已变得非常重要。 如果设备驱动程序附带了错误的版本号或使用错误格式的版本号，则在安装任何 DirectX 应用程序时，最终用户会遇到困难。

**注意****DriverVer** 指令提供一种将驱动程序包的版本信息（包括驱动程序文件和 inf 文件本身）添加到 INF 文件的方法。 通过使用和更新 **DriverVer** 指令，驱动程序包可以安全且最终地替换为同一包的未来版本。 有关此指令的详细信息，请参阅 Windows 驱动程序工具包 (WDK) 文档的 "设备安装" 部分中的 INF DriverVer 指令。

下表提供了适用于 IHV 或 OEM 提供的驱动程序的版本号的范围，以便与各种版本的 DirectX 兼容。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">目标系统</th>
<th align="left">版本号
<div>
 
</div>
发件人：</th>
<th align="left">版本号
<div>
 
</div>
向上直到：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>仅限 Windows 98 的驱动程序 (DirectX5) </p></td>
<td align="left"><p>4.05.00.0000</p></td>
<td align="left"><p>4.05.00.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>DirectX 1.0 兼容的驱动程序</p></td>
<td align="left"><p>4.02.00.0095</p></td>
<td align="left"><p>4.03.00.1096</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DirectX 2.0 兼容的驱动程序</p></td>
<td align="left"><p>4.03.00.1096</p></td>
<td align="left"><p>4.03.00.2030</p></td>
</tr>
<tr class="even">
<td align="left"><p>DirectX 3.0 兼容的驱动程序</p></td>
<td align="left"><p>4.03.00.2030</p></td>
<td align="left"><p>4.04.00.0000</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DirectX 5.0 兼容的驱动程序</p></td>
<td align="left"><p>4.10.10.0000</p></td>
<td align="left"><p>4.10.10.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>DirectX 6.0 兼容的驱动程序</p></td>
<td align="left"><p>4.11.10.0000</p></td>
<td align="left"><p>4.11.10.9999</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows 98/Me DirectX 7.0 兼容的驱动程序</p></td>
<td align="left"><p>4.12.10.0000</p></td>
<td align="left"><p>4.12.10.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 2000 DirectX 7.0-兼容驱动程序</p></td>
<td align="left"><p>5.12.10.0000</p></td>
<td align="left"><p>5.12.10.9999</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows XP 和更高版本的 DirectX 7.0 兼容驱动程序</p></td>
<td align="left"><p>6.12.10.0000</p></td>
<td align="left"><p>6.12.10.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 98/Me DirectX 8.0 兼容的驱动程序</p></td>
<td align="left"><p>4.13.10.0000</p></td>
<td align="left"><p>4.13.10.9999</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows 2000 DirectX 8.0-兼容驱动程序</p></td>
<td align="left"><p>5.13.10.0000</p></td>
<td align="left"><p>5.13.10.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows XP 和更高版本的 DirectX 8.0 兼容驱动程序</p></td>
<td align="left"><p>6.13.10.0000</p></td>
<td align="left"><p>6.13.10.9999</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows 98/Me DirectX 9.0 兼容的驱动程序</p></td>
<td align="left"><p>4.14.10.0000</p></td>
<td align="left"><p>4.14.10.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 2000 DirectX 9.0-兼容驱动程序</p></td>
<td align="left"><p>5.14.10.0000</p></td>
<td align="left"><p>5.14.10.9999</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows XP 和更高版本的 DirectX 9.0 兼容驱动程序</p></td>
<td align="left"><p>6.14.10.0000</p></td>
<td align="left"><p>6.14.10.9999</p></td>
</tr>
</tbody>
</table>

 

**注意**   DirectX 9.0 DDK 文档表明 Windows XP 和更高版本的 DirectX 兼容驱动程序的版本号必须介于6之间。*nn*. 01.0000 到6。*nn*. 01.9999。 但是，若要支持旧版的 WHQL 手动测试规范，文档还表明版本号可能为6。*nn*. 10.0000 到6。*nn*. 10.9999。
由于这种传统的 WHQL 要求，某些 DirectX 应用程序需要显示驱动程序版本号 *n*。*nn*. 10。*nnnn*。 如果显示驱动程序的版本号已从 *n* 切换。*nn*. 10。*nnnn* 到 *n*。*nn*. 01。*nnnn* ，使其更准确地符合 DIRECTX 9.0 DDK 文档要求，此类应用程序可能不会运行，因为它们会将驱动程序解释为早期版本。

因此，显示驱动程序的版本号应设置为 *n*。*nn*. 10。*nnnn*。

 

对于不支持 DirectX 的设备驱动程序，版本号必须大于4.00.00.0095 且小于4.02.00.0095。 例如，如果显示设备驱动程序是 Windows 3.1 显示器驱动程序或仅限 Windows 95 的显示驱动程序，则版本号4.01.00.0000 是正确的。

相反，此驱动程序的版本号4.03.00.0000 不正确。 仅在 Windows 95 上支持 DirectX 的设备驱动程序的版本号应等于或大于4.02.00.0095 且小于4.04.00.0000。

### <a name="span-idstoring_internal_version_numbersspanspan-idstoring_internal_version_numbersspanstoring-internal-version-numbers"></a><span id="storing_internal_version_numbers"></span><span id="STORING_INTERNAL_VERSION_NUMBERS"></span>存储内部版本号

除了 Microsoft 在版本号上所需的格式之外，许多供应商已将存储内部版本号的需求表示为产品支持和测试目的。 每个 DirectX 驱动程序都有一个存储在副本中的版本号：一个二进制版本作为2个 Dword 存储，一个字符串版本。 不能修改二进制版本。

不过，可以通过以下方式追加字符串版本：

1.  供应商创建版本号，如本文前面所述。 此版本号在二进制版本号中按 "原样" 使用。

2.  供应商使用此版本号作为字符串版本号的基础。 如果需要，可将特定于供应商的版本字符串追加到现有版本号，以形成完整的字符串版本号。 特定于供应商的字符串和版本号之间用 "-" (连字符) 。

例如，如果 "4.03.00.2100" 是符合 DirectX 标准的显示驱动程序的版本号，并且供应商在内部使用 "xx. xx. xx. xx" 数字格式，则驱动程序中的组合字符串版本号将是 "4.03.00.2100"。

当客户通过右键单击 Windows 资源管理器中的文件，选择 " **属性**"，然后单击 " **版本** " 选项卡) 来检查驱动程序的版本号 (，Windows 将显示字符串版本。 供应商的产品支持人员应能够标识版本编号的供应商特定部分（如果有）并采取适当的措施。

 

 





