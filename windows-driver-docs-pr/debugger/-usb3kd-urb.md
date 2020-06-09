---
title: usb3kd.urb
description: Usb3kd. urb 扩展显示有关 USB 请求块（URB）的信息。
ms.assetid: B4583F32-BBC9-4182-A403-9C43BBD9BA4F
keywords:
- usb3kd urb Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.urb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 55f149cab615cf496ae91cb861c760b0db372fe0
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534152"
---
# <a name="usb3kdurb"></a>!usb3kd.urb


[**！ Usb3kd urb**](-usb3kd-device-info.md)扩展显示有关 USB 请求块（urb）的信息。

```dbgcmd
!usb3kd.urb UrbAddress
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______UrbAddress______"></span><span id="_______urbaddress______"></span><span id="_______URBADDRESS______"></span>*UrbAddress*   
URB 的地址。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usb3kd

<a name="examples"></a>示例
--------

下面的示例显示了在[**！ xhci \_ deviceslots**](-usb3kd-xhci-deviceslots.md)命令的输出中的 URB （0xfffffa8005a2cbe8）的地址。

```dbgcmd
3: kd> !xhci_deviceslots 0xfffffa800520d2d0

## Dumping dt _DEVICESLOT_DATA 0xfffffa8003612e80
----------------------------------------------
DeviceContextBase: VA 0xfffffa8005a64000 LA 0x116864000 !wdfcommonbuffer 0x57ffa7ca758 Size 4096

## [1] SlotID : dt USBXHCI!_USBDEVICE_DATA 0xfffffa80059027d0 dt _SLOT_CONTEXT32 0xfffffa8005a65000
------------------------------------------------------------------------------------------------
    USB\VID_...
    SlotEnabled IsDevice NumberOfTTs 0 TTThinkTime 0
    ...
            PendingTransferList: 
                [0] dt _TRANSFER_DATA 0xfffffa80059727f0 !urb 0xfffffa8005a2cbe8 !wdfrequest 0x57ffa68d998 TransferState_Pending
    ...
```

下面的示例将 URB 的地址传递给 **！ usb3kd**命令。

```dbgcmd
3: kd> !urb 0xfffffa8005a2cbe8

## Dumping URB 0xfffffa8005a2cbe8
------------------------------
Function:         URB_FUNCTION_BULK_OR_INTERRUPT_TRANSFER (0x9)
UsbdDeviceHandle: 
    !ucx_device 0xfffffa8005901840
    !xhci_deviceslots 0xfffffa800520d2d0 1

Status:           USBD_STATUS_PENDING (0x40000000)
UsbdFlags:        (0x0)
dt _URB_BULK_OR_INTERRUPT_TRANSFER 0xfffffa8005a2cbe8
PipeHandle:            0xfffffa800596f720
TransferFlags:         (0x1) USBD_TRANSFER_DIRECTION_IN
TransferBufferLength:  0x0
TransferBuffer:        0xfffffa8005a2cc88
TransferBufferMDL:     0xfffffa8005848930
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[通用串行总线（USB）驱动程序](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






