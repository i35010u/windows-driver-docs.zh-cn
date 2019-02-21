---
title: LowerLogoVersion
description: LowerLogoVersion
ms.assetid: b11b9190-9e3f-473d-b78f-b472601c60e2
keywords:
- LowerLogoVersion
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9590339d89be7b99c7dce4b5bb25f7e64a4ad4f1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543875"
---
# <a name="lowerlogoversion"></a>LowerLogoVersion


**LowerLogoVersion**是[设备安装程序类属性](https://msdn.microsoft.com/library/windows/hardware/ff542239)的签名对分数的影响的驱动程序，如下所示：

-   Windows 将最佳签名分数分配给具有相同的 Windows 版本的 WHQL 签名的驱动程序或更高版本比**LowerLogoVersion**值。

-   Windows 将下一步最佳签名分数分配给第三方进行签名的驱动程序使用验证码技术和 Windows 版本的 WHQL 签名的驱动程序到早于**LowerLogoVersion**值。

一个**LowerLogoVersion**值是一个以 NULL 结尾的字符串，指定 Windows 版本中下, 表中所示。

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

 

系统默认值**LowerLogoVersion**系统定义的值[设备安装程序类](device-setup-classes.md)"5.1。" 这意味着 Windows Server 2003 和 Windows XP 具有 WHQL 签名的驱动程序具有相同的签名分数作为由 Microsoft 为 Windows Vista 和更高版本的 Windows 签名的驱动程序。

有关驱动程序分级的详细信息，请参阅[如何 Windows Ranks Drivers （Windows Vista 和更高版本）](how-setup-ranks-drivers--windows-vista-and-later-.md)。

 

 





