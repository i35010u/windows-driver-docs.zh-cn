---
title: 映射 Netmap.inf 文件中的 Id
description: 映射 Netmap.inf 文件中的 Id
ms.assetid: 7cab4aa1-8b0b-4cdc-a093-b91be6170961
keywords:
- 网络组件升级，WDK，netmap.inf 文件
- 升级网络组件 WDK，netmap.inf 文件
- netmap.inf 文件 WDK
- 映射网络组件 Id
- ID 映射 WDK netmap.inf
- 设备 Id WDK netmap.inf
- 供应商提供的文件 WDK netmap.inf 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3a4342a2285ad86a97619b78b68baee07ee2a14
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555406"
---
# <a name="mapping-ids-in-a-netmapinf-file"></a>映射 Netmap.inf 文件中的 Id





**请注意**  供应商提供网络升级不支持在 Microsoft Windows XP (SP1 和更高版本)，Microsoft Windows Server 2003 和更高版本操作系统。

 

Netmap.inf 文件包含一个或多个以下顶级部分。 每个部分包含中列出的组件的 ID 映射**映射**列。

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

 

部分中的每个条目映射网络组件的升级前的设备，硬件或兼容 ID 到其相应的 Windows 2000 或更高版本 id。 每个条目指定任一配置文件*一对一*ID 映射或*一个多*ID 映射。 介绍了以下的这些映射策略。

网络客户端未在 Windows NT 3.51 和 Windows NT 4.0; 这种情况下定义因此，如果前面的网络服务变得的网络客户端在 Windows 2000 或更高版本，其设备 ID 映射必须列在**OemNetClients**部分中，不能在**OemNetServices**部分。

 

 





