---
title: 连接到并行端口的设备的物理配置
description: 连接到并行端口的设备的物理配置
keywords:
- IEEE 1284 WDK
- 并行端口 WDK，设备配置
- 菊花链设备 WDK
- 并行设备 WDK，物理配置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7614a999956272d1542567668ca35a6f122541da
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806109"
---
# <a name="physical-configuration-of-devices-attached-to-a-parallel-port"></a>连接到并行端口的设备的物理配置





本部分介绍附加到并行端口的设备的典型物理配置。

下图显示了连接并行端口的并行设备。

![阐释连接到并行端口的并行设备的示意图](images/parport2.png)

Microsoft Windows 支持将一台并行设备连接到并行端口，该设备可以是旧设备，也可以是符合 IEEE 1284 标准的即插即用设备。

下图显示了 IEEE 1284.3 设备以及同时附加到并行端口的链上 IEEE 1284 设备。

![连接到并行端口的 ieee 1284.3 菊花链设备](images/parport3.png)

IEEE 1284.3 标准指定最多四个菊花链设备，最后一个链设备可以同时连接到并行端口。

下表指定每个版本的 Windows 支持的 IEEE 1284.3 设备的数目。

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
<th>菊花链设备的最大数量</th>
<th>IEEE 1284.3 设备 Id</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Me</p></td>
<td><p>零</p></td>
<td><p>空值</p></td>
<td><p>系统提供的驱动程序不支持。</p></td>
</tr>
<tr class="even">
<td><p>Windows 2000</p></td>
<td><p>four</p></td>
<td><p>从0到3</p></td>
<td><p>为了确保可靠操作，Microsoft 建议在最多两台设备上进行操作。</p></td>
</tr>
<tr class="odd">
<td><p>Windows XP 及更高版本</p></td>
<td><p>two</p></td>
<td><p>0 或 1</p></td>
<td></td>
</tr>
</tbody>
</table>

 

有关支持 IEEE 1284.3 设备的详细信息，请参阅：

[并行设备接口、内部名称和符号链接](parallel-device-interfaces--internal-names--and-symbolic-links.md)

[选择和取消选择连接到并行端口的 IEEE 1284 设备](selecting-and-deselecting-an-ieee-1284-device-attached-to-a-parallel-p.md)

 

 




