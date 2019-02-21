---
title: 各种外形规格的实现需求
description: 本主题介绍各种外形规格的实现需求。
ms.assetid: F14E9811-B432-409B-B7AD-262C2DD76C25
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5258792f41cd95ad657126de2226c193a78b4f20
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545789"
---
# <a name="implementation-requirements-for-various-form-factors"></a>各种外形规格的实现需求


本主题介绍各种外形规格的实现需求。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"></th>
<th align="left">外形尺寸</th>
<th align="left">定义</th>
<th align="left">GPIO 指示器实现要求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><img src="images/slate.jpg" alt="Slate" /></p></td>
<td align="left">静态图像</td>
<td align="left">使用任何可附加键盘的平板电脑外形规格</td>
<td align="left">提供静态停靠附件时，必须实现停靠的指示器。</td>
</tr>
<tr class="even">
<td align="left"><p><img src="images/laptop.jpg" alt="Laptop" /></p></td>
<td align="left">便携式计算机</td>
<td align="left">永久连接始终是可用于键入的键盘。</td>
<td align="left">以静态方式将模式设置为便携式计算机。</td>
</tr>
<tr class="odd">
<td align="left"><p><img src="images/convertible.jpg" alt="Convertible" /></p></td>
<td align="left">变形本</td>
<td align="left">可用作一台平板电脑或平板电脑的系统。 可以分离、 翻转或 swivelled 键盘。</td>
<td align="left"><p>实现的便携式计算机/盖板指示器。</p>
<p>如果保持静止的停靠附件不可用，还必须实现停靠的指示器。</p></td>
</tr>
<tr class="even">
<td align="left"><p><img src="images/allinone.jpg" alt="All-in-One" /></p></td>
<td align="left">-一体</td>
<td align="left">中等大小桌面/部 portable 系统具有附件作为附加的键盘。</td>
<td align="left">没有必需的因为键盘是可选的附件的实现。</td>
</tr>
</tbody>
</table>

 

 

 




