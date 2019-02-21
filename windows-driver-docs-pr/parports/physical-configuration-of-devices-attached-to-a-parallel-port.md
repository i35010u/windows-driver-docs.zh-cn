---
title: 连接到并行端口设备的物理配置
description: 连接到并行端口设备的物理配置
ms.assetid: ae90fcc6-7ea8-4cb1-89a1-1fbf1ad5c05e
keywords:
- IEEE 1284 WDK
- 并行端口 WDK，设备配置
- 菊花链设备 WDK
- 并行 WDK，物理配置的设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2a18430701f9a851b06f06f9bb2ab2364cdf4b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547094"
---
# <a name="physical-configuration-of-devices-attached-to-a-parallel-port"></a>连接到并行端口设备的物理配置





本部分介绍了附加到并行端口设备的典型物理配置。

下图显示了并行设备附加并行端口。

![说明并行连接到并行端口设备的关系图](images/parport2.png)

Microsoft Windows 支持一个并行的设备连接旧设备或符合 IEEE 1284 标准的即插设备可以是在并行端口。

下图显示了 IEEE 1284.3 设备和一个最终的链 IEEE 1284 设备，同时连接到并行端口。

![ieee 1284.3 菊花链设备连接到并行端口](images/parport3.png)

IEEE 1284.3 标准规定，最多四个菊花链设备和最终的链设备可以同时附加到并行端口。

下表指定支持的每个版本的 Windows 的 IEEE 1284.3 设备数。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>Windows 版本</th>
<th>最大菊花链设备数</th>
<th>IEEE 1284.3 设备 Id</th>
<th>备注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Me</p></td>
<td><p>zero</p></td>
<td><p>不适用</p></td>
<td><p>不支持系统提供的驱动程序。</p></td>
</tr>
<tr class="even">
<td><p>Windows 2000</p></td>
<td><p>四个</p></td>
<td><p>从 0 到 3</p></td>
<td><p>若要确保可靠的操作，Microsoft 建议最多两个设备。</p></td>
</tr>
<tr class="odd">
<td><p>Windows XP 及更高版本</p></td>
<td><p>二</p></td>
<td><p>0 或 1</p></td>
<td></td>
</tr>
</tbody>
</table>

 

支持 IEEE 1284.3 设备的详细信息，请参阅：

[并行设备接口、 内部名称和符号链接](parallel-device-interfaces--internal-names--and-symbolic-links.md)

[选择和取消选择附加到并行端口的 IEEE 1284 设备](selecting-and-deselecting-an-ieee-1284-device-attached-to-a-parallel-p.md)

 

 




