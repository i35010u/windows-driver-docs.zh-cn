---
title: devext
description: Devext 扩展在各种总线上显示设备的特定于总线的设备扩展信息。
keywords:
- 'usbhub 扩展 (过时) '
- 'hidfdo 扩展 (过时) '
- 'hidpdo 扩展 (过时) '
- 设备扩展
- 公交车
- devext Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- devext
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 313cf462c8c05408fd7aedc62610f2b8b796239c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815251"
---
# <a name="devext"></a>!devext


**！ Devext** extension 显示各种总线上设备的特定于总线的设备扩展信息。

```dbgcmd
!devext Address TypeCode
```

## <a name="span-idddk__devext_dbgspanspan-idddk__devext_dbgspanparameters"></a><span id="ddk__devext_dbg"></span><span id="DDK__DEVEXT_DBG"></span>参数

###  <a name="address"></a>*Address*   
指定要显示的设备扩展的十六进制地址。

#### <a name="typecode"></a>*TypeCode*   
指定拥有要显示的设备扩展的对象的类型。 类型代码不区分大小写。 有效的类型代码是：

|TypeCode|对象|
|--- |--- |
|ISAPNP|ISA PnP 设备扩展|
|PCMCIA|PCMCIA 设备扩展|
|HID|HID 设备扩展|
 

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll
 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

请参阅 [即插即用调试](plug-and-play-debugging.md) 此扩展命令的应用程序。 有关设备扩展的详细信息，请参阅 Windows 驱动程序工具包 (WDK) 文档。

<a name="remarks"></a>备注
-------

**！ Usbhub**， **！ hidfdo**， **！ hidpdo** extension 已过时;它们的功能已集成到 **！ devext**。

对于不再受 **！ devext** 支持的对象类型，请使用 [**Dt (显示类型)**](dt--display-type-.md) 调试器命令。

下面是一个 ISA PnP 设备扩展示例：

```dbgcmd
kd> !devext e0000165fff32190 ISAPNP
ISA PnP FDO @ 0x00000000, DevExt @ 0xe0000165fff32190, Bus # 196639
Flags (0x854e2530)  DF_ACTIVATED, DF_QUERY_STOPPED, 
                    DF_STOPPED, DF_RESTARTED_NOMOVE, 
                    DF_BUS
                    Unknown flags 0x054e2000

NumberCSNs           - -536870912
ReadDataPort         - 0x0000000d (mapped)
AddressPort          - 0x00000000 (not mapped)
CommandPort          - 0x00000000 (not mapped)
DeviceList           - 0xe000000085007b50
CardList             - 0x00000000
PhysicalBusDevice    - 0x00000000
AttachedDevice       - 0x00000000
SystemPowerState     - Unspecified
DevicePowerState     - Unspecified
```

下面是 PCI 设备的示例：

```dbgcmd
kd> !devext e0000000858c31b0 PCI
PDO Extension, Bus 0x0, Device 0, Function 0.
  DevObj 0xe0000000858c3060 PCI Parent Bus FDO DevExt 0xe0000000858c4960
  Device State = PciNotStarted
  Vendor ID 8086 (INTEL)  Device ID 123D
  Class Base/Sub 08/00  (Base System Device/Interrupt Controller)
  Programming Interface: 20, Revision: 01, IntPin: 00, Line Raw/Adj 00/00
  Enables ((cmd & 7) = 106): BM   Capabilities Pointer = <none>
  CurrentState:          System Working,  Device D0
  WakeLevel:             System Unspecified,  Device Unspecified
  Requirements: <none>
```

 

 





