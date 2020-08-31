---
title: LowerLogoVersion
description: LowerLogoVersion
ms.assetid: b11b9190-9e3f-473d-b78f-b472601c60e2
keywords:
- LowerLogoVersion
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9670c9956af0aa310ae70fa5aac05c54e2ab432f
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095919"
---
# <a name="lowerlogoversion"></a>LowerLogoVersion


**LowerLogoVersion** 是一个 [设备安装程序类属性](/previous-versions/ff542239(v=vs.85)) ，它会影响驱动程序的签名分数，如下所示：

-   Windows 将最佳签名评分分配给具有与 **LowerLogoVersion** 值相同或更晚的 Windows 版本的 WHQL 签名的驱动程序。

-   Windows 将下一个最佳签名评分分配给由第三方使用 Authenticode 技术签名的驱动程序，并将其分配给具有早于 **LowerLogoVersion** 值的 Windows 版本的 WHQL 签名的驱动程序。

**LowerLogoVersion**值是以 NULL 结尾的字符串，它指定 Windows 版本，如下表所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows 版本</th>
<th align="left">LowerLogoVersion 值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Windows 7</p></td>
<td align="left"><p>6.1</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows Server 2008</p></td>
<td align="left"><p>6.1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Vista</p></td>
<td align="left"><p>6.0</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows Server 2003</p></td>
<td align="left"><p>5.2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows XP</p></td>
<td align="left"><p>5.1</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 2000</p></td>
<td align="left"><p>5.0</p></td>
</tr>
</tbody>
</table>

 

系统定义的[设备安装程序类](./overview-of-device-setup-classes.md)的系统默认**LowerLogoVersion**值为 "5.1"。 这意味着，具有 Windows Server 2003 和 Windows XP WHQL 签名的驱动程序与 Microsoft 为 Windows Vista 和更高版本的 Windows 签名的驱动程序具有相同的签名分数。

有关驱动程序排名的详细信息，请参阅 [windows (Windows Vista 和更高版本) 的驱动程序的方式 ](how-setup-ranks-drivers--windows-vista-and-later-.md)。

 

