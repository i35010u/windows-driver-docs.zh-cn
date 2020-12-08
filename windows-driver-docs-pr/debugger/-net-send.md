---
title: net_send
description: Net_send 扩展通过本地网络发送消息。
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
ms.openlocfilehash: cb299a78db4edb12360af4ef8b1cafeb89db9cf2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803311"
---
# <a name="net_send"></a>！ net \_ send


**！ Net \_ 发送** 扩展通过本地网络发送消息。

```dbgcmd
!net_send SendingMachine TargetMachine Sender Message
```

## <a name="span-idddk__net_send_dbgspanspan-idddk__net_send_dbgspanparameters"></a><span id="ddk__net_send_dbg"></span><span id="DDK__NET_SEND_DBG"></span>参数


<span id="_______SendingMachine______"></span><span id="_______sendingmachine______"></span><span id="_______SENDINGMACHINE______"></span>*SendingMachine*   
指定将处理命令的计算机。 建议将此名称设置为运行调试器的计算机的名称，因为网络配置可能会拒绝发送消息。 *SendingMachine* 不应 (中包含前导反斜杠 \\ \) 。

<span id="_______TargetMachine______"></span><span id="_______targetmachine______"></span><span id="_______TARGETMACHINE______"></span>*TargetMachine*   
指定将消息发送到的计算机。 *TargetMachine* 不应 (中包含前导反斜杠 \\ \) 。

<span id="_______Sender______"></span><span id="_______sender______"></span><span id="_______SENDER______"></span>*发件人*   
指定邮件的发件人。 建议 *发送方* 与 *SendingMachine* 相同，因为网络配置可能拒绝发送消息。 显示消息时，此字符串将被标识为消息的发件人。

<span id="_______Message______"></span><span id="_______message______"></span><span id="_______MESSAGE______"></span>*消息*   
指定消息本身。 *发件人* 参数后的所有文本都将被视为 *消息* 的一部分，包括空格和引号，尽管 [**分号**](----command-separator-.md)将终止 *消息* 并开始新的命令。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

 

 





