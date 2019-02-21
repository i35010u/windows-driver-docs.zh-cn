---
title: HBA\_状态
description: HBA\_状态
ms.assetid: 2fabfa86-7f8a-4c90-8aa0-53e42bd5c075
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 47421b11a79fdd3433cca28230e55831b7911376
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521026"
---
# <a name="hbastatus"></a>HBA\_状态


## <span id="ddk_hba_status_kr"></span><span id="DDK_HBA_STATUS_KR"></span>


HBA\_状态 WMI 类限定符表示 WMI 请求对 WMI 提供程序 HBA 所做的结果。

下表列出了限定符名称和每个名称的含义：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">限定符</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>HBA_STATUS_OK</p></td>
<td align="left"><p>HBA 上检测到任何错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR</p></td>
<td align="left"><p>HBA 上检测到错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_NOT_SUPPORTED</p></td>
<td align="left"><p>不支持的函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_INVALID_HANDLE</p></td>
<td align="left"><p>无效句柄。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_ARG</p></td>
<td align="left"><p>错误的参数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_ILLEGAL_WWN</p></td>
<td align="left"><p>无法识别的全球通用名称。 有关与全球通用名称有关的信息，请参阅 T11 委员会&#39;s<em>光纤通道 HBA API</em>规范。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_ILLEGAL_INDEX</p></td>
<td align="left"><p>无法识别的索引。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_MORE_DATA</p></td>
<td align="left"><p>需要更大的缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_STALE_DATA</p></td>
<td align="left"><p>自最后一次刷新操作以来已更改的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_SCSI_CHECK_CONDITION</p></td>
<td align="left"><p>SCSI 检查报告的情况。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_BUSY</p></td>
<td align="left"><p>适配器正忙还是保留，可能还需要重试。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_TRY_AGAIN</p></td>
<td align="left"><p>请求已超时，可能需要重试。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_UNAVAILABLE</p></td>
<td align="left"><p>已删除或停用被引用的 HBA。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_ELS_REJECT</p></td>
<td align="left"><p>请求的 ELS 拒绝了本地适配器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_INVALID_LUN</p></td>
<td align="left"><p>指定的适配器不提供指定的 LUN。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_INCOMPATIBLE</p></td>
<td align="left"><p>已检测到不兼容。 库和驱动程序的模块可能已实现 HBA API 规范的不同的版本。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_AMBIGUOUS_WWN</p></td>
<td align="left"><p>多个适配器具有匹配的全球通用名称 (WWN)。 如果多个适配器 NodeWWN 是完全相同，这可能发生。 有关一般情况下的信息与全球范围内有关名称和 NodeWWN 特别是，请参阅 T11 委员会&#39;s<em>光纤通道 HBA API</em>规范。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_LOCAL_BUS</p></td>
<td align="left"><p>永久绑定请求包含错误的本地 SCSI 总线数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_LOCAL_TARGET</p></td>
<td align="left"><p>永久绑定请求包含错误的本地 SCSI 目标数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_LOCAL_LUN</p></td>
<td align="left"><p>永久绑定请求包含错误的本地 SCSI LUN。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_LOCAL_SCSIID_BOUND</p></td>
<td align="left"><p>永久绑定集请求包含一个已绑定的本地 SCSI ID。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_TARGET_FCID</p></td>
<td align="left"><p>永久绑定请求包含无效 FCP 目标 FCID。 FCID FCP 目标的定义，请参阅 T11 委员会&#39;s<em>光纤通道 HBA API</em>规范。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_TARGET_NODE_WWN</p></td>
<td align="left"><p>永久绑定请求包含错误的 FCP 目标节点 WWN。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_TARGET_PORT_WWN</p></td>
<td align="left"><p>永久绑定请求包含错误的 FCP 目标端口的 WWN。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_TARGET_LUN</p></td>
<td align="left"><p>永久绑定请求包含目标不能识别 FCP LUN。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_TARGET_LUID</p></td>
<td align="left"><p>永久绑定请求包含一个未定义，或者无法访问逻辑单元的唯一标识符。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_NO_SUCH_BINDING</p></td>
<td align="left"><p>永久绑定删除请求包含与由指定的端口建立的绑定不匹配绑定。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_NOT_A_TARGET</p></td>
<td align="left"><p>SCSI 命令发送到不是 SCSI 目标端口 Nx_Port。 Nx_Port 的定义，请参阅 T11 委员会&#39;s<em>光纤通道 HBA API</em>规范。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_UNSUPPORTED_FC4</p></td>
<td align="left"><p>发出了有关不受支持的 FC 4 协议的请求。 FC 4 协议的说明，请参阅 T11 委员会&#39;s<em>光纤通道 HBA API</em>规范。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_INCAPABLE</p></td>
<td align="left"><p>已请求来启用端口未实现的功能。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_TARGET_BUSY</p></td>
<td align="left"><p>执行请求的 SCSI 命令将导致重叠的 SCSI 命令条件。</p></td>
</tr>
</tbody>
</table>

 

通过包括*Hbaapi.h*您的软件有权访问一系列的对应于上表中的类型名称的符号常量。 这些符号常量的定义中不包括*Hbapiwmi.h* （WMI 工具套件时对其进行编译，生成的文件）。

 

 





