---
title: 常用、 相机和扫描程序属性
description: 常用、 相机和扫描程序属性
ms.assetid: 7d988a1b-4c2f-43f7-be09-a250d9ede35c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4325b3ea9918e5e03669860fde32add1da1bc879
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555485"
---
# <a name="common-camera-and-scanner-properties"></a>常用、 相机和扫描程序属性





WIA 属性是设备 （根） 或 （子级） 的项的属性。 设备属性包含有关该设备，如制造商的名称、 设备和其类型 （扫描仪或照相机） 的说明信息。 项属性包含有关某个特定项，如时捕获，项的名称等信息。 设备属性由 WIA\_D 命名约定; 项属性由 WIA 标识\_我命名约定。

三个字母首字母缩略词中间 WIA 属性名称包含有关属性的类型的信息： 它是通用设备信息属性 (DIP)、 （DPA、 DPC 或分发点） 的设备属性或 item 属性 （IPA、 IPC 或 IP）。 设备和项属性可以是这两种类型的设备 （DPA 和 IPA） 通用的、 可以是特定于照相机 （DPC 或 IPC） 也可以是特定于扫描程序 （DPS 和 IP）。 下表列出了各种 WIA 属性类型，并提供了每种类型的示例。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性类型</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_DIP_<em>Xxx</em></p></td>
<td><p>设备信息属性</p>
<p>安装程序和安装信息普遍适用于扫描仪和照相机的设备。 WIA 服务提供了这些属性。 微型驱动程序不提供它们。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPA_<em>Xxx</em></p></td>
<td><p>设备属性，所有</p>
<p>普遍适用于扫描仪和照相机的设备，例如连接状态和设备时间的信息。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_<em>Xxx</em></p></td>
<td><p>项属性，所有</p>
<p>普遍适用于照相机和扫描仪的项，例如项目的信息&#39;名称和图像的类型。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPC_<em>Xxx</em></p></td>
<td><p>设备属性照相机</p>
<p>特定于照相机设备，如拍摄图片的数量的信息。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPC_<em>Xxx</em></p></td>
<td><p>Item 属性照相机</p>
<p>特定于照相机项，如缩略图图像的宽度和高度的信息。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_<em>Xxx</em></p></td>
<td><p>设备属性，扫描程序</p>
<p>特定于扫描程序设备，如平台大小的信息。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_<em>Xxx</em></p></td>
<td><p>Item 属性，扫描程序</p>
<p>它是特定于扫描程序项，例如水平和垂直分辨率的信息。</p></td>
</tr>
</tbody>
</table>

 

请参阅[WIA 属性](https://msdn.microsoft.com/library/windows/hardware/ff552739)有关 WIA 常见、 特定于照相机的和特定于扫描程序的属性的完整列表。

 

 




