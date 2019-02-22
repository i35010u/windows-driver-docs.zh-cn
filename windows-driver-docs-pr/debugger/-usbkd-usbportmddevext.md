---
title: usbkd.usbportmddevext
description: 如果一个 usbport _DEVICE_EXTENSION 结构是中的故障转储中已存在该 usbkd.usbportmddevext 命令显示结果生成 Bug 检查 0xFE。
ms.assetid: 07DE5D4A-E909-4D9B-B906-B74C9CC8AE49
keywords:
- usbkd.usbportmddevext Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbportmddevext
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fd1a1006d7cc08652a696506e38b191368ab2726
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546715"
---
# <a name="usbkdusbportmddevext"></a>!usbkd.usbportmddevext


**！ Usbkd.usbportmddevext**命令将显示**usbport ！\_设备\_扩展**结构，如果结果是生成的故障转储中存在[ **Bug 检查 0xFE**](bug-check-0xfe--bugcode-usb-driver.md)。

```dbgcmd
!usbkd.usbportmddevext
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="remarks"></a>备注
-------

使用此命令仅在调试时为生成的崩溃转储文件[ **Bug 检查 0xFE:BUGCODE\_USB\_驱动程序**](bug-check-0xfe--bugcode-usb-driver.md)。

<a name="examples"></a>示例
--------

下面是输出的示例 **！ usbportmddevext**。

```dbgcmd
1: kd> !analyze -v
*** ...
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
    **Power and Wake -----------------------------------------------
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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






