---
title: Netmap.inf 文件中的映射 ID
description: Netmap.inf 文件中的映射 ID
keywords:
- 网络组件升级 WDK，netmap .inf 文件
- 升级网络组件 WDK，netmap .inf 文件
- netmap 文件 WDK
- 映射网络组件 Id
- ID 映射 WDK netmap
- 设备 Id WDK netmap
- 供应商提供的文件 WDK netmap 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41c204c12dbce3332186ea9d68b72dc094bec829
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833355"
---
# <a name="mapping-ids-in-a-netmapinf-file"></a>Netmap.inf 文件中的映射 ID





**注意**  Microsoft Windows XP (SP1 及更高版本) 、Microsoft Windows Server 2003 和更高版本的操作系统不支持供应商提供的网络升级。

 

Netmap 文件包含一个或多个以下顶级部分。 每个部分都包含 " **映射** " 列中列出的组件的 ID 映射。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">部分</th>
<th align="left">映射</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>OemNetAdapters</strong></p></td>
<td align="left"><p>网络适配器，不包括异步适配器</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>OemAsyncAdapters</strong></p></td>
<td align="left"><p>异步网络适配器</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>OemNetProtocols</strong></p></td>
<td align="left"><p>网络协议驱动程序</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>OemNetServices</strong></p></td>
<td align="left"><p>网络服务</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>OemNetClients</strong></p></td>
<td align="left"><p>网络客户端</p></td>
</tr>
</tbody>
</table>

 

部分中的每个条目将网络组件的 preupgrade 设备、硬件或兼容 ID 映射到其对应的 Windows 2000 或更高版本的 ID。 每个条目均指定 *一对一* *id 映射或一对多* id 映射。 下面介绍了这些映射策略。

网络客户端未在 Windows NT 3.51 和 Windows NT 4.0 中进行定义，因此，如果早期的网络服务成为 Windows 2000 或更高版本下的网络客户端，则其设备 ID 映射必须在 **OemNetClients** 节中列出，而不是在 **OemNetServices** 节中列出。

 

 





