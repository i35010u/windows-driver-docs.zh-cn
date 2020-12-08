---
title: NVGRE 任务卸载的标准化 INF 关键字
description: 本部分介绍用于支持 NVGRE 的驱动程序的 INF 文件中使用的标准化关键字
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32b20d19ab7e12b9d4f14aebd171b9554a75a1f9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792619"
---
# <a name="standardized-inf-keywords-for-nvgre-task-offload"></a>NVGRE 任务卸载的标准化 INF 关键字


定义 **\* EncapsulatedPacketTaskOffload** 标准化枚举关键字，以启用或禁用对 [使用通用路由封装的网络虚拟化的支持 (NVGRE)](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)微型端口适配器中的任务卸载。

下表描述了此关键字可能的 INF 条目。

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
<th align="left">“值”</th>
<th align="left">EnumDesc</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>*EncapsulatedPacketTaskOffload</strong></p></td>
<td align="left"><p>封装任务卸载</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p>
（默认值）</td>
<td align="left"><p>已启用</p></td>
</tr>
</tbody>
</table>

 

有关标准化 INF 关键字的详细信息，请参阅 [网络设备的标准化 Inf 关键字](standardized-inf-keywords-for-network-devices.md)。

 

 





