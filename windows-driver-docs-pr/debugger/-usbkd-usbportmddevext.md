---
title: usbkd.usbportmddevext
description: Usbkd usbportmddevext 命令显示 usbport _DEVICE_EXTENSION 结构（如果在作为结果 Bug 检查0xFE 生成的故障转储中存在）。
keywords:
- usbkd usbportmddevext Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbportmddevext
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5fe307ecc4294273b75eafb9edf661c448bf1e8f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833889"
---
# <a name="usbkdusbportmddevext"></a>!usbkd.usbportmddevext


**！ Usbkd. usbportmddevext** 命令显示 **usbport！ \_设备 \_ 扩展** 结构（如果在作为结果 [**Bug 检查 0xFE**](bug-check-0xfe--bugcode-usb-driver.md)生成的故障转储中存在）。

```dbgcmd
!usbkd.usbportmddevext
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd.dll

<a name="remarks"></a>备注
-------

仅当调试因 [**Bug 检查0xFE： BUGCODE \_ USB \_ 驱动程序**](bug-check-0xfe--bugcode-usb-driver.md)而生成的故障转储文件时，才使用此命令。

<a name="examples"></a>示例
--------

下面是 **！ usbportmddevext** 的输出示例。

```dbgcmd
1: kd> !analyze -v
**_ ...
BUGCODE_USB_DRIVER (fe) 
...
1: kd> !usbkd.usbportmddevext
USBPORT.SYS DEVICE_EXTENSION DATA: 
Hcd FDO Extension:
Sig:4f444648 HFDO
CurrentPnpFunc: 0x00000008
PnpFuncHistoryIdx: 0x0000000d
CurrentPowerFunc: 0x00000000
PowerFuncHistoryIdx: 0x00000000
PnpLogIdx: 0x00000002
IoRequestCount: 0x00000007
IoRequestAsyncCallbackCount: 0xffffffff
IoRequestAllow: 0x00000000
Pnp Func History (idx 13)
...
[02] pnp 13 (0d) IRP_MN_FILTER_RESOURCE_REQUIREMENTS
[...
Power Func History (idx 0)
[01] pnp 255 (ff) ??? (x0) PowerDeviceUnspecified
...
    _*Power and Wake -----------------------------------------------
    selective suspend:on (1)
    PowerFlags (00000080):
*---FDO---*
PMDebug: 0x00000000
MinAllocedBw: 0x00000000
MaxAllocedBw: 0x00000000
## ...

## XDPC HISTORY_UsbHcIntDpc

State History (idx 2)
EVENT, STATE, NEXT 
Log[3] @ 000000d9e7c615cc  
Ev_Xdpc_Worker       XDPC_DpcQueued          XDPC_Running            
## ...        

## XDPC HISTORY_UsbDoneDpc

State History (idx 0)
EVENT, STATE, NEXT 
Log[1] @ 000000d9e7c61774  
Ev_Xdpc_Worker       XDPC_DpcQueued          XDPC_Running            
## ...          

## XDPC HISTORY_UsbMapDpc

State History (idx 3)
EVENT, STATE, NEXT 
Log[4] @ 000000d9e7c6196c  
## ...         

## XDPC HISTORY_UsbIocDpc

State History (idx 0)
EVENT, STATE, NEXT 
Log[1] @ 000000d9e7c61b04  
Ev_Xdpc_Worker       XDPC_DpcQueued          XDPC_Running            
...           
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

