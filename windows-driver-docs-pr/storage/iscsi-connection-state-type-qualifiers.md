---
title: ISCSI\_连接\_状态\_类型\_限定符
description: ISCSI\_连接\_状态\_类型\_限定符
ms.assetid: 53242205-4fd3-471d-abe2-35474491b29d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: de5a7bebe25dc2c725ef2cd32e8b8078db200dff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520335"
---
# <a name="iscsiconnectionstatetypequalifiers"></a>ISCSI\_连接\_状态\_类型\_限定符


## <span id="ddk_iscsi_connection_state_type_qualifiers_kr"></span><span id="DDK_ISCSI_CONNECTION_STATE_TYPE_QUALIFIERS_KR"></span>


ISCSI\_连接\_状态\_类型\_限定符 WMI 属性限定符对应于一组表示连接状态的值。

下表描述了 ISCSI\_连接\_状态\_类型\_限定符值。

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
<td align="left"><p>连接为在登录请求阶段。 已建立连接，但目标仍未发送的最后一位集的有效的登录响应。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>目标已发送的最后一位集的有效的登录响应，该连接是在完整的功能阶段中，发起方可以将 SCSI 命令和数据发送到目标。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>发起方发送有效注销命令，但尚未关闭连接。</p></td>
</tr>
</tbody>
</table>

 

 

 





