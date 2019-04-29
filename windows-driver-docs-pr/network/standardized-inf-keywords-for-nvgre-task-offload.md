---
title: 有关 NVGRE 任务卸载的标准化的 INF 关键字
description: 本部分介绍支持 NVGRE 的驱动程序的 INF 文件中使用的标准化的关键字
ms.assetid: C1FB0519-6BB7-46B0-A3FA-B8E982279C44
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99dd3b002389b3844b0f68ef21c750d00ba91893
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345967"
---
# <a name="standardized-inf-keywords-for-nvgre-task-offload"></a>NVGRE 任务卸载的标准化 INF 关键字


 **\*EncapsulatedPacketTaskOffload**标准化的枚举关键字定义来启用或禁用对支持[使用通用路由封装 (NVGRE) 任务卸载的网络虚拟化](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)微型端口适配器中。

下表说明了此关键字可能 INF 条目。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">ReplTest1</th>
<th align="left">EnumDesc</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>*EncapsulatedPacketTaskOffload</strong></p></td>
<td align="left"><p>封装的任务卸载</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p>
“(默认)”</td>
<td align="left"><p>Enabled</p></td>
</tr>
</tbody>
</table>

 

有关标准化 INF 关键字的详细信息，请参阅[为网络设备的标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)。

 

 





