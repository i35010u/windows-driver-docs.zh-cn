---
title: rcdrkd.rcdrsettraceprefix
description: Rcdrkd. rcdrsettraceprefix 扩展设置跟踪消息前缀。
keywords:
- rcdrkd rcdrsettraceprefix Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rcdrkd.rcdrsettraceprefix
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 26f78c78c6bbd29bfa393ed1cd186cfb0078143a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821019"
---
# <a name="rcdrkdrcdrsettraceprefix"></a>!rcdrkd.rcdrsettraceprefix


**！ Rcdrkd rcdrsettraceprefix** 扩展设置跟踪消息前缀。

```dbgcmd
!rcdrkd.rcdrsettraceprefix TracePrefixString 
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______TracePrefixString______"></span><span id="_______traceprefixstring______"></span><span id="_______TRACEPREFIXSTRING______"></span>*TracePrefixString*   
跟踪消息的前缀字符串。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Rcdrkd.dll

<a name="remarks"></a>备注
-------

记录器日志中的每条消息都有前缀，可以通过指定跟踪消息前缀字符串来控制。 有关详细信息，请参阅 [跟踪消息前缀](../devtest/trace-message-prefix.md)。

<a name="examples"></a>示例
--------

在下面的示例中，跟踪消息前缀最初为 **%7！ u！：%！求!-** . 参数 **%7！ u！** 指定前缀包括消息序列号。 参数 **%！FUNC！** 指定前缀包含生成消息的函数的名称。 该示例调用 **！ rcdrsettraceprefix** 将前缀字符串更改为 **%7！ u！**。 之后，日志显示包含消息序列号，但不包括函数名称。

```dbgcmd
0: kd> !rcdrlogdump USBXHCI -a 0xfffffa8010737b60
Trace searchpath is: 

Trace format prefix is: %7!u!: %!FUNC! - 
Trying to extract TMF information from - C:\ProgramData\dbg\sym\usbxhci.pdb\D4C85D5D3E2843879EDE226A334D69552\usbxhci.pdb
--- start of log ---
405: TransferRing_DispatchEventsAndReleaseLock - 1.8.1: Mapping Begin : Path 1 TransferRingState_Mapping Events 0x00000000
406: TransferRing_StageRetrieveFromRequest - 1.8.1: WdfRequest 0x0000057FEE117A88 TransferData 0xFFFFFA8011EE8700 Function 0x9 Length 500 TransferSize 500 BytesProcessed 0
...
---- end of log ----

0: kd> !rcdrsettraceprefix %7!u!: 
SetTracePrefix: "%7!u!: "
0: kd> !rcdrlogdump USBXHCI -a 0xfffffa8010737b60
Trace searchpath is: 

Trace format prefix is: %7!u!: 
Trying to extract TMF information from - C:\ProgramData\dbg\sym\usbxhci.pdb\D4C85D5D3E2843879EDE226A334D69552\usbxhci.pdb
--- start of log ---
405: 1.8.1: Mapping Begin : Path 1 TransferRingState_Mapping Events 0x00000000
406: 1.8.1: WdfRequest 0x0000057FEE117A88 TransferData 0xFFFFFA8011EE8700 Function 0x9 Length 500 TransferSize 500 BytesProcessed 0
...
---- end of log ----
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[RCDRKD 扩展](rcdrkd-extensions.md)

 

