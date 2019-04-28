---
title: rcdrkd.rcdrsettraceprefix
description: Rcdrkd.rcdrsettraceprefix 扩展设置的跟踪消息前缀。
ms.assetid: BFA987B8-7013-4112-A674-064ED59741C0
keywords:
- rcdrkd.rcdrsettraceprefix Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rcdrkd.rcdrsettraceprefix
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a59aaf44176e80aa450a0f99efe799b1a9a1f932
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334324"
---
# <a name="rcdrkdrcdrsettraceprefix"></a>!rcdrkd.rcdrsettraceprefix


**！ Rcdrkd.rcdrsettraceprefix**扩展设置的跟踪消息前缀。

```dbgcmd
!rcdrkd.rcdrsettraceprefix TracePrefixString 
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______TracePrefixString______"></span><span id="_______traceprefixstring______"></span><span id="_______TRACEPREFIXSTRING______"></span> *TracePrefixString*   
跟踪消息前缀字符串。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Rcdrkd.dll

<a name="remarks"></a>备注
-------

录制器日志中的每个消息都有一个可以控制由指定的跟踪消息前缀字符串的前缀。 有关详细信息，请参阅[跟踪消息前缀](https://msdn.microsoft.com/library/windows/hardware/ff553941)。

<a name="examples"></a>示例
--------

在以下示例中，跟踪消息前缀是最初 **%7 ！ u ！: %！FUNC ！-** . 参数 **%7 ！ u ！** 指定前缀，包括消息序列号。 参数 **%！FUNC ！** 指定前缀，包括生成消息的函数的名称。 此示例调用 **！ rcdrsettraceprefix**若要更改的前缀字符串 **%7 ！ u ！**。 在此之后，显示日志包括消息序列号，但不包括函数名称。

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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[RCDRKD 扩展](rcdrkd-extensions.md)

 

 






