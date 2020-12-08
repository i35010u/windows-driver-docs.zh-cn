---
title: HBA \_ 状态
description: HBA \_ 状态
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 49f1f895616e8210c95c913f99300a73b402a302
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835183"
---
# <a name="hba_status"></a>HBA \_ 状态


## <span id="ddk_hba_status_kr"></span><span id="DDK_HBA_STATUS_KR"></span>


HBA \_ 状态 WMI 类限定符指示对 wmi 提供程序 HBA 发出的 wmi 请求的结果。

下表列出了每个名称的限定符名称和含义：

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
<td align="left"><p>在 HBA 上未检测到任何错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR</p></td>
<td align="left"><p>在 HBA 上检测到错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_NOT_SUPPORTED</p></td>
<td align="left"><p>功能不受支持。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_INVALID_HANDLE</p></td>
<td align="left"><p>句柄无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_ARG</p></td>
<td align="left"><p>参数错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_ILLEGAL_WWN</p></td>
<td align="left"><p>全球名称无法识别。 有关全球名称的信息，请参阅 T11 委员会 <em>光纤通道 HBA API</em> 规范。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_ILLEGAL_INDEX</p></td>
<td align="left"><p>无法识别索引。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_MORE_DATA</p></td>
<td align="left"><p>需要更大的缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_STALE_DATA</p></td>
<td align="left"><p>自上次刷新操作后的信息已更改。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_SCSI_CHECK_CONDITION</p></td>
<td align="left"><p>已报告 SCSI 检查条件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_BUSY</p></td>
<td align="left"><p>适配器繁忙或已保留，可能需要重试。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_TRY_AGAIN</p></td>
<td align="left"><p>请求已超时，可能需要重试。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_UNAVAILABLE</p></td>
<td align="left"><p>引用的 HBA 已被删除或停用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_ELS_REJECT</p></td>
<td align="left"><p>请求的 ELS 被本地适配器拒绝。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_INVALID_LUN</p></td>
<td align="left"><p>指定的适配器未提供指定的 LUN。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_INCOMPATIBLE</p></td>
<td align="left"><p>检测到不兼容。 库和驱动程序模块可能已经实现了不同版本的 HBA API 规范。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_AMBIGUOUS_WWN</p></td>
<td align="left"><p>多个适配器的全球通用名称 (WWN) 。 如果多个适配器的 NodeWWN 相同，则可能会发生这种情况。 有关全球通用名称和 NodeWWN 的详细信息，请参阅 T11 委员会 <em>光纤通道 HBA API</em> 规范。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_LOCAL_BUS</p></td>
<td align="left"><p>永久性绑定请求包含错误的本地 SCSI 总线号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_LOCAL_TARGET</p></td>
<td align="left"><p>永久性绑定请求包含错误的本地 SCSI 目标编号。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_LOCAL_LUN</p></td>
<td align="left"><p>永久性绑定请求包含错误的本地 SCSI LUN。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_LOCAL_SCSIID_BOUND</p></td>
<td align="left"><p>永久性绑定集请求包含已绑定的本地 SCSI ID。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_TARGET_FCID</p></td>
<td align="left"><p>永久性绑定请求包含无效的 FCP 目标 FCID。 有关 FCP 目标 FCID 的定义，请参阅 T11 委员会的 <em>光纤通道 HBA API</em> 规范。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_TARGET_NODE_WWN</p></td>
<td align="left"><p>永久性绑定请求包含错误的 FCP 目标节点 WWN。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_TARGET_PORT_WWN</p></td>
<td align="left"><p>永久性绑定请求包含错误的 FCP 目标端口 WWN。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_TARGET_LUN</p></td>
<td align="left"><p>永久性绑定请求包括目标无法识别的 FCP LUN。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_TARGET_LUID</p></td>
<td align="left"><p>永久性绑定请求包含未定义的或无法访问的逻辑单元唯一标识符。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_NO_SUCH_BINDING</p></td>
<td align="left"><p>永久性绑定删除请求包含的绑定与指定端口建立的绑定不匹配。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_NOT_A_TARGET</p></td>
<td align="left"><p>SCSI 命令发送到的 Nx_Port 不是 SCSI 目标端口。 有关 Nx_Port 的定义，请参阅 T11 委员会的 <em>光纤通道 HBA API</em> 规范。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_UNSUPPORTED_FC4</p></td>
<td align="left"><p>针对不受支持的 FC-SW 协议发出的请求。 有关 FC-SW 协议的说明，请参阅 T11 委员会 <em>光纤通道 HBA API</em> 规范。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_INCAPABLE</p></td>
<td align="left"><p>发出了为端口启用未实现功能的请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_TARGET_BUSY</p></td>
<td align="left"><p>执行请求的 SCSI 命令会导致 SCSI 重叠的命令条件。</p></td>
</tr>
</tbody>
</table>

 

通过包含 *Hbaapi* ，你的软件将有权访问与上表中的类型名称对应的一系列符号常量。 这些符号常量的定义不包含在 *Hbapiwmi* 中， (WMI 工具套件编译) 时生成的文件。

 

 





