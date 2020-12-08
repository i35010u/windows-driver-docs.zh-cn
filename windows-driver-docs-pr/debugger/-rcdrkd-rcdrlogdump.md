---
title: rcdrkd.rcdrlogdump
description: Rcdrkd. rcdrlogdump 扩展显示驱动程序或驱动程序集的所有记录器缓冲区中的跟踪消息。
keywords:
- rcdrkd rcdrlogdump Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rcdrkd.rcdrlogdump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 63cb4008deb1a995dec186ed20bfc1d64625f5ec
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821017"
---
# <a name="rcdrkdrcdrlogdump"></a>!rcdrkd.rcdrlogdump


**！ Rcdrkd rcdrlogdump** 扩展显示驱动程序或驱动程序集的所有记录器缓冲区中的跟踪消息。

```dbgcmd
!rcdrkd.rcdrlogdump DriverName [DriverName ...]
!rcdrkd.rcdrlogdump DriverName -a Address
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DriverName______"></span><span id="_______drivername______"></span><span id="_______DRIVERNAME______"></span>*DriverName*   
驱动程序的名称，不包括 .sys 扩展。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
如果指定 Address，则此命令将显示指定地址处的日志缓冲区中的跟踪消息。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Rcdrkd.dll

<a name="examples"></a>示例
--------

下面的示例显示 **！ rcdrlogdump** 命令的一部分输出。

```dbgcmd
3: kd> !rcdrlogdump usbxhci.sys
Trace searchpath is: 

Trace format prefix is: %7!u!: %!FUNC! - 
Log dump command                           Log ID                   Size
================                           ======                   ====
!rcdrlogdump  usbxhci -a fffffa8005ff2b60  03 SLT02 DCI04           1024
!rcdrlogdump  usbxhci -a fffffa8005ff2010  03 SLT02 DCI03           1024
!rcdrlogdump  usbxhci -a fffffa8005b36010  03 SLT01 DCI03           1024
!rcdrlogdump  usbxhci -a fffffa8005b379e0  03 SLT01 DCI04           1024
!rcdrlogdump  usbxhci -a fffffa8005b33350  03 SLT02 DCI01           1024
!rcdrlogdump  usbxhci -a fffffa8005b2bb60  03 SLT01 DCI01           1024
!rcdrlogdump  usbxhci -a fffffa8005a2bb60  03 CMD                   1024
!rcdrlogdump  usbxhci -a fffffa8005a1ab60  03 INT00                 1024
!rcdrlogdump  usbxhci -a fffffa8005085330  03 RUNDOWN               512
!rcdrlogdump  usbxhci -a fffffa8005311780  03 1033 0194             1024
Trying to extract TMF information from - C:\ProgramData\dbg\sym\usbxhci.pdb\D4C85D5D3E2843879EDE226A334D69552\usbxhci.pdb
--- start of log ---
03 RUNDOWN     6: Controller_RetrievePciData - PCI Bus.Device.Function: 48.0.0
03 RUNDOWN     7: Controller_RetrievePciData - PCI: VendorId 0x1033 DeviceId 0x0194 RevisionId 0x03
03 RUNDOWN     8: Controller_QueryDeviceFlagsFromKse - Found DeviceFlags 0x101800 for USBXHCI:PCI\VEN_1033&DEV_0194
03 RUNDOWN     9: Controller_RetrieveDeviceFlags - DeviceFlags 0x101804
...
03 SLT01 DCI03 89911: TransferRing_DispatchEventsAndReleaseLock - 1.3.0: Mapping Complete : Path 1 TransferRingState_Idle Events 0x00000000
03 SLT01 DCI04 89912: TransferRing_DispatchEventsAndReleaseLock - 1.4.0: Mapping Begin : Path 3 TransferRingState_Mapping Events 0x00000000
03 SLT01 DCI04 89913: TransferRing_DispatchEventsAndReleaseLock - 1.4.0: Mapping Complete : Path 3 TransferRingState_Idle Events 0x00000000
---- end of log ----
```

前面的输出包含来自多个日志缓冲区的消息。 若要查看单个日志缓冲区中的消息，请使用 **-a** 参数，并指定日志缓冲区的地址。 下面的示例演示如何在地址 fffffa8005ff2b60 的日志缓冲区中显示消息。

```dbgcmd
3: kd> !rcdrlogdump  usbxhci -a fffffa8005ff2b60
Trace searchpath is: 

Trace format prefix is: %7!u!: %!FUNC! - 
Trying to extract TMF information from - C:\ProgramData\dbg\sym\usbxhci.pdb\D4C85D5D3E2843879EDE226A334D69552\usbxhci.pdb
--- start of log ---
70914: TransferRing_DispatchEventsAndReleaseLock - 2.4.0: Mapping Complete : Path 1 TransferRingState_Idle Events 0x00000000
70916: TransferRing_TransferEventHandler - 2.4.0: TransferEventTrb 0xFFFFFA8005A3FBF0 CC_SUCCESS Length 31 EventData 1 Pointer 0xfffffa8005b96210
70917: TransferRing_TransferEventHandler - 2.4.0: WdfRequest 0x0000057FFA469FD8 transferData 0xFFFFFA8005B961B0
70918: TransferRing_TransferComplete - 2.4.0: WdfRequest 0x0000057FFA469FD8 completed with STATUS_SUCCESS BytesProcessed 31
70922: TransferRing_DispatchEventsAndReleaseLock - 2.4.0: Mapping Begin : Path 3 TransferRingState_Mapping Events 0x00000000
70923: TransferRing_DispatchEventsAndReleaseLock - 2.4.0: Mapping Complete : Path 3 TransferRingState_Idle Events 0x00000000
81064: TransferRing_DispatchEventsAndReleaseLock - 2.4.0: Mapping Begin : Path 1 TransferRingState_Mapping Events 0x00000000
81065: TransferRing_StageRetrieveFromRequest - 2.4.0: WdfRequest 0x0000057FFA469FD8 TransferData 0xFFFFFA8005B961B0 Function 0x9 Length 31 TransferSize 31 BytesProcessed 0
81066: TransferRing_DispatchEventsAndReleaseLock - 2.4.0: Mapping Complete : Path 1 TransferRingState_Idle Events 0x00000000
81068: TransferRing_TransferEventHandler - 2.4.0: TransferEventTrb 0xFFFFFA8005A40270 CC_SUCCESS Length 31 EventData 1 Pointer 0xfffffa8005b96210
81069: TransferRing_TransferEventHandler - 2.4.0: WdfRequest 0x0000057FFA469FD8 transferData 0xFFFFFA8005B961B0
81070: TransferRing_TransferComplete - 2.4.0: WdfRequest 0x0000057FFA469FD8 completed with STATUS_SUCCESS BytesProcessed 31
81074: TransferRing_DispatchEventsAndReleaseLock - 2.4.0: Mapping Begin : Path 3 TransferRingState_Mapping Events 0x00000000
81075: TransferRing_DispatchEventsAndReleaseLock - 2.4.0: Mapping Complete : Path 3 TransferRingState_Idle Events 0x00000000
---- end of log ----
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[RCDRKD 扩展](rcdrkd-extensions.md)

 

 






