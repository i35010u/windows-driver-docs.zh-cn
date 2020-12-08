---
title: 常用属性、相机属性和扫描仪属性
description: 常用属性、相机属性和扫描仪属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a485a68cfb4567c8976363564b76a05bdec73c2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823177"
---
# <a name="common-camera-and-scanner-properties"></a>常用属性、相机属性和扫描仪属性





WIA 属性是设备 (根) 或 (子) 项的特性。 设备属性包含有关设备的信息，如制造商的名称、设备说明，以及设备 (扫描仪或照相机) 的类型。 项属性包含特定项的相关信息，例如项的名称、捕获时间等。 设备属性由 WIA \_ D 命名约定标识; 项属性由 wia \_ I 命名约定标识。

WIA 属性名称中间有三个字母的首字母缩写词，其中包含有关属性类型的信息： (DIP) 、设备属性 (DPA、DPC 或 DPS) ，或 (IPA、IPC 或 IPS) 的项目属性。 设备和项属性可以通用于两种类型的设备 (DPA 和 IPA) ，可以特定于相机 (DPC 或 IPC) ，也可以特定于扫描仪 (DPS 和 IP) 。 下表列出了各种 WIA 属性类型，并提供了每种类型的示例。

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
<p>扫描仪和照相机设备通用的设置和安装信息。 WIA 服务提供这些属性。 微型驱动程序不提供这些功能。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPA_<em>Xxx</em></p></td>
<td><p>设备属性，所有</p>
<p>扫描仪和照相机设备共有的信息，例如连接状态和设备时间。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_<em>Xxx</em></p></td>
<td><p>Item 属性，All</p>
<p>照相机和扫描仪项共有的信息，如项的名称和图像的类型。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPC_<em>Xxx</em></p></td>
<td><p>设备属性，照相机</p>
<p>照相机设备特定的信息，例如拍摄的图片数。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPC_<em>Xxx</em></p></td>
<td><p>Item 属性，照相机</p>
<p>特定于照相机项目的信息，例如缩略图图像的宽度和高度。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_<em>Xxx</em></p></td>
<td><p>设备属性，扫描器</p>
<p>特定于扫描仪设备的信息，如床大小。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_<em>Xxx</em></p></td>
<td><p>项目属性，扫描器</p>
<p>特定于扫描仪项目的信息，例如水平和垂直分辨率。</p></td>
</tr>
</tbody>
</table>

 

请参阅 [Wia Properties](./wia-properties.md) ，获取 wia 常见、特定于相机和特定于扫描仪的属性的完整列表。

 

