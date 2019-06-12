---
title: usbkd.usbhubpd
description: Usbkd.usbhubpd 命令显示有关 USB 端口的信息。
ms.assetid: 41D5E65D-76C2-45E0-9AC7-C2B50D806935
keywords:
- usbkd.usbhubpd Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhubpd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cdae55164518d2eebca7536d038f55a9d32fc61d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340607"
---
# <a name="usbkdusbhubpd"></a>!usbkd.usbhubpd


**！ Usbkd.usbhubpd**命令显示有关 USB 端口的信息。

```dbgcmd
!usbkd.usbhubpd StructAddr
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span> *StructAddr*   
地址**usbhub ！\_集线器\_端口\_数据**结构。 若要获取这些结构的地址，请使用[ **！ usbhubext**](-usbkd-usbhubext.md)。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是一种方法，若要查找的地址**usbhub ！\_集线器\_端口\_数据**。 首次进入[ **！ usbkd.usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
    RootHub !hub2_info ffffe000023201a0 !devstack ffffe00002320050
        ...
```

在上面的输出中可以看到建议的命令 **！ devstack ffffe00002320050**。 输入此命令。

```dbgcmd
0: kd> !kdexts.devstack ffffe00002320050

  !DevObj           !DrvObj            !DevExt           ObjectName
> ffffe00002320050  \Driver\usbhub     ffffe000023201a0  0000002d
  ffffe0000213c050  \Driver\usbehci    ffffe0000213c1a0  USBPDO-3
...
```

在上面的输出，您可以看到的中心的 FDO 设备扩展的地址是`ffffe000023201a0`。

传递到设备扩展的地址[ **！ usbhubext** ](-usbkd-usbhubext.md)命令。

```dbgcmd
0: kd> !usbkd.usbhubext ffffe000023201a0

FDO ffffe00002320050 PDO ffffe0000213c050 HubNumber# 3
dt USBHUB!_DEVICE_EXTENSION_HUB ffffe000023201a0
!usbhublog ffffe000023201a0
RemoveLock ffffe00002320668
FdoFlags ffffe00002320ba0

CurrentPowerIrp: System (0000000000000000) Device (0000000000000000)
...
## PORT DATA

PortData 1: !port2_info ffffe000021bf000 Port State = PS_WAIT_CONNECT PortChangeLock: 0, Pcq_State: Pcq_Run_Idle             
     PDO 0000000000000000 
....
```

在上面的输出`ffffe000021bf000`是地址 **\_中心\_端口\_数据**结构。 传递到此地址 **！ usbhubpd**。

```dbgcmd
0: kd> !usbkd.usbhubpd ffffe000021bf000
PortNumber: 1
Parent Hub FDO ffffe00002320050
Device PDO <NULL>
dt USBHUB!_HUB_PORT_DATA ffffe000021bf000
dt USBHUB!_PORTDATA_FLAGS ffffe000021bf968

PortChangelist: !usblist ffffe000021bf1c8, CL [Empty]

## Port Indicators Log (latest at bottom)

##     Event           State                Next

    [EMPTY]

## Port Change Queue History (latest at bottom)

##     Event                State                    Next                     PcqEv_Suspend PcqEv_Resume  PcqEv_ChDone  Tag 

01. PCE_Resume           Pcq_Stop                 Pcq_Pause                              PcqEv_Reset   PcqEv_Reset   REQUEST_RESUME     
...          Pcq_Run_wBusy            Pcq_Run_Idle                                                                            

## Port Status History (latest at bottom)

##     Current State          Change Eve nt        PDO              CEOSP H/W Port REG Frame Inserted

01. PS_WAIT_CONNECT        REQUEST_PAUSE       0000000000000000 00000 100  Age:000 512498
...
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






