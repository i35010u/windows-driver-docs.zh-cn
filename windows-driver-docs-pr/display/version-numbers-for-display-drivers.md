---
title: 显示驱动程序的版本号
description: 显示驱动程序的版本号
ms.assetid: 73d26532-61c1-45d1-a388-7c0befc53487
keywords:
- 显示版本号 WDK Windows 2000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4dabe47e0f30e73e63831039886eebbcffd33a32
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390756"
---
# <a name="version-numbers-for-display-drivers"></a>显示驱动程序的版本号


## <span id="ddk_ensuring_correct_version_numbers_gg"></span><span id="DDK_ENSURING_CORRECT_VERSION_NUMBERS_GG"></span>


若要确保最终用户可以使用显示器驱动程序特定的操作系统上和与特定版本的 DirectX，相应的版本号必须应用于该驱动程序。 使用 DirectX，版本号已变得非常重要的设备驱动程序。 如果设备驱动程序随版本错误号或使用格式不正确的版本号，最终用户在安装任何 DirectX 应用程序时将时遇到问题。

**请注意** **DriverVer**指令提供了一种方法，若要添加的驱动程序包，其中包括驱动程序文件和 INF 文件本身，到 INF 文件版本信息。 通过使用并更新**DriverVer**指令，驱动程序包可以安全地确定地替换为同一个包的未来版本。 有关此指令的详细信息，请参阅 Windows Driver Kit (WDK) 文档的设备安装部分中的 INF DriverVer 指令。

下表提供的适用于 IHV 或 OEM 提供的驱动程序的版本编号的范围与各种版本的 DirectX 的兼容性。

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
经过：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>仅限 Windows 98 的驱动程序 (DirectX5)</p></td>
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
<td align="left"><p>Windows 98 / 我的 DirectX 7.0 兼容的驱动程序</p></td>
<td align="left"><p>4.12.10.0000</p></td>
<td align="left"><p>4.12.10.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 2000 DirectX 7.0 兼容的驱动程序</p></td>
<td align="left"><p>5.12.10.0000</p></td>
<td align="left"><p>5.12.10.9999</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows XP 和更高版本的 DirectX 7.0 兼容驱动程序</p></td>
<td align="left"><p>6.12.10.0000</p></td>
<td align="left"><p>6.12.10.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 98 / 我的 DirectX 8.0 兼容的驱动程序</p></td>
<td align="left"><p>4.13.10.0000</p></td>
<td align="left"><p>4.13.10.9999</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows 2000 DirectX 8.0 兼容的驱动程序</p></td>
<td align="left"><p>5.13.10.0000</p></td>
<td align="left"><p>5.13.10.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows XP 和更高版本的 DirectX 8.0 兼容驱动程序</p></td>
<td align="left"><p>6.13.10.0000</p></td>
<td align="left"><p>6.13.10.9999</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows 98 / 我的 DirectX 9.0 兼容的驱动程序</p></td>
<td align="left"><p>4.14.10.0000</p></td>
<td align="left"><p>4.14.10.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 2000 DirectX 9.0 兼容的驱动程序</p></td>
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

 

**请注意**   DirectX 9.0 DDK 文档所指示的 Windows XP 及更高版本的 DirectX 兼容驱动程序的版本号必须介于 6。*nn*.01.0000 到 6。*nn*.01.9999。 但是，若要支持旧 WHQL 手动测试规范，文档还指示版本号可能从 6。*nn*.10.0000 到 6。*nn*.10.9999。
由于此旧 WHQL 需求，某些 DirectX 应用程序所需的显示驱动程序版本号*n*。*nn*.10。*nnnn*。 如果显示驱动程序的版本号从切换*n*。*nn*.10。*nnnn*到*n*。*nn*.01。*nnnn* ，以便更准确地遵守 DirectX 9.0 DDK 文档要求，因为它们将解释为早期版本的驱动程序，此类应用程序可能无法运行。

因此，显示器驱动程序的版本号应设置为*n*。*nn*.10。*nnnn*。

 

不支持 DirectX 的设备驱动程序，版本号必须大于 4.00.00.0095 且小于 4.02.00.0095。 例如，如果显示设备驱动程序，Windows 3.1 显示驱动程序或仅限 Windows 95 的显示驱动程序版本号为 4.01.00.0000 会是正确的。

相反，此驱动程序的 4.03.00.0000 版本号会不正确。 仅在 Windows 95 上支持 DirectX 的设备驱动程序应具有等于或大于 4.02.00.0095 且小于 4.04.00.0000 版本号。

### <a name="span-idstoringinternalversionnumbersspanspan-idstoringinternalversionnumbersspanstoring-internal-version-numbers"></a><span id="storing_internal_version_numbers"></span><span id="STORING_INTERNAL_VERSION_NUMBERS"></span>存储内部版本号

除了 Microsoft 要求来表示版本号的格式，许多供应商具有表示您要存储的产品支持的内部版本号和测试目的。 每个 DirectX 驱动程序有一个存储中重复的版本号： 一个存储为两个 dword 值的二进制版本和一个字符串版本。 不能修改二进制版本。

但是，可以按以下方式追加字符串版本：

1.  供应商创建的版本号，如本文前面部分中所述。 此版本号"按原样"中使用二进制版本数。

2.  供应商使用此版本号的字符串版本号作为基础。 如果需要，可以将特定于供应商的版本字符串追加到现有的版本编号，以形成完整的字符串版本号。 特定于供应商的字符串和版本号分隔"-"（连字符字符）。

例如，如果"4.03.00.2100"是 DirectX 符合要求的显示驱动程序的版本号和供应商在内部使用"xx.xx.xx"数字格式，驱动程序中的组合的字符串版本号是"4.03.00.2100-xx.xx.xx"。

当客户将检查驱动程序的版本号 (通过右键单击文件在 Windows 资源管理器中，选择**属性**，然后单击**版本**选项卡)，Windows 显示的字符串版本。 供应商的产品支持应能够识别的版本号的特定于供应商的部分，如果它存在并采取相应措施。

 

 





