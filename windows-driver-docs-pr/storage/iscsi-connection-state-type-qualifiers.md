---
title: ISCSI \_ 连接 \_ 状态 \_ 类型 \_ 限定符
description: ISCSI \_ 连接 \_ 状态 \_ 类型 \_ 限定符
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6609b1b777c00216432319a90569293819b689db
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835145"
---
# <a name="iscsi_connection_state_type_qualifiers"></a>ISCSI \_ 连接 \_ 状态 \_ 类型 \_ 限定符


## <span id="ddk_iscsi_connection_state_type_qualifiers_kr"></span><span id="DDK_ISCSI_CONNECTION_STATE_TYPE_QUALIFIERS_KR"></span>


ISCSI \_ 连接 \_ 状态 \_ 类型 \_ 限定符 WMI 属性限定符对应于一组表示连接状态的值。

下表描述了 ISCSI \_ 连接 \_ 状态 \_ 类型 \_ 限定符值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">连接状态值</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>连接在 "登录请求" 阶段。 已建立连接，但目标仍未发送最终位集的有效登录响应。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>目标已经发送了一个有效的登录响应，并设置了最后一个位，该连接处于完全功能阶段，发起方可以向目标发送 SCSI 命令和数据。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>发起方发送了有效的注销命令，但连接尚未关闭。</p></td>
</tr>
</tbody>
</table>

 

 

 





