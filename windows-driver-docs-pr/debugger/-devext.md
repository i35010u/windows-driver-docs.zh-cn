---
title: devext
description: Devext 扩展显示各种总线上的总线特定于设备的设备的扩展信息。
ms.assetid: b4d4f595-9b0b-40e2-8790-2c913a50c8fe
keywords:
- usbhub 扩展 （已过时）
- hidfdo 扩展 （已过时）
- hidpdo 扩展 （已过时）
- 设备扩展
- 总线
- devext Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- devext
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 81d31c09168df2ea28d43674313cfc2644cfcb52
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576704"
---
# <a name="devext"></a>!devext


**！ Devext**扩展各种总线上显示特定于总线的设备的设备的扩展信息。

```dbgcmd
!devext Address TypeCode
```

## <a name="span-idddkdevextdbgspanspan-idddkdevextdbgspanparameters"></a><span id="ddk__devext_dbg"></span><span id="DDK__DEVEXT_DBG"></span>参数

###  <a name="address"></a>*地址*   
指定要显示的设备扩展的十六进制地址。

#### <a name="typecode"></a>*TypeCode*   
指定拥有设备扩展要显示对象的类型。 类型代码，不区分大小写。 有效的类型代码为：

|TypeCode|对象|
|--- |--- |
|ISAPNP|ISA 即插即用设备扩展|
|PCMCIA|PCMCIA 设备扩展|
|HID|HID 的设备扩展|
 

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll
 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

请参阅[插调试](plug-and-play-debugging.md)对于此扩展命令的应用程序。 有关设备扩展的详细信息，请参阅 Windows Driver Kit (WDK) 文档。

<a name="remarks"></a>备注
-------

**！ Usbhub**， **！ hidfdo**，并 **！ hidpdo**扩展已过时; 其功能已集成到 **！ devext**。

有关这些对象不再支持的类型 **！ devext**，使用[ **dt （显示类型）** ](dt--display-type-.md)调试器命令。

下面是 ISA 即插即用设备扩展的示例：

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

下面是一个示例，用于 PCI 设备：

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

 

 





