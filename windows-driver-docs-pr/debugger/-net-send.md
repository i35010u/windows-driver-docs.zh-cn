---
title: net_send
description: Net_send 扩展本地网络上发送消息。
ms.assetid: 13d5fe3f-6477-4610-8928-020726ccb3c8
keywords:
- 网络消息
- net_send Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- net_send
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: be6e30c5a3abe6024ac5edefc6dc383d86d7873a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335863"
---
# <a name="netsend"></a>!net\_send


**！ Net\_发送**扩展本地网络上发送一条消息。

```dbgcmd
!net_send SendingMachine TargetMachine Sender Message
```

## <a name="span-idddknetsenddbgspanspan-idddknetsenddbgspanparameters"></a><span id="ddk__net_send_dbg"></span><span id="DDK__NET_SEND_DBG"></span>参数


<span id="_______SendingMachine______"></span><span id="_______sendingmachine______"></span><span id="_______SENDINGMACHINE______"></span> *SendingMachine*   
指定将处理该命令的计算机。 建议这是调试器运行，因为你的网络配置可能会拒绝否则发送消息的计算机的名称。 *SendingMachine*不应包括前导反斜杠 (\\\)。

<span id="_______TargetMachine______"></span><span id="_______targetmachine______"></span><span id="_______TARGETMACHINE______"></span> *TargetMachine*   
指定将向其发送消息的计算机。 *TargetMachine*不应包括前导反斜杠 (\\\)。

<span id="_______Sender______"></span><span id="_______sender______"></span><span id="_______SENDER______"></span> *Sender*   
指定消息的发件人。 建议*发件人*应该与相同*SendingMachine*，因为你的网络配置可能会拒绝否则发送消息。 当显示消息时，此字符串将被标识为消息的发件人。

<span id="_______Message______"></span><span id="_______message______"></span><span id="_______MESSAGE______"></span> *消息*   
指定消息本身。 之后的所有文本*发件人*参数将被视为属于*消息*，其中包括空格和引号，尽管[**分号**](----command-separator-.md)将终止*消息*并开始新的命令。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

 

 





