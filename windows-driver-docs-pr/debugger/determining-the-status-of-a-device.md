---
title: 确定设备的状态
description: 确定设备的状态
ms.assetid: d250643e-13cb-4657-9235-5fdeb1eab89a
keywords:
- Plug and Play (PnP) 设备状态
- Plug and Play (PnP) 设备树
- 设备状态
- 设备树
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f0ea19c5aa6debf255e44106cf2d7b3b6c74f1e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532968"
---
# <a name="determining-the-status-of-a-device"></a>确定设备的状态


## <span id="ddk_determining_the_status_of_a_device_dbg"></span><span id="DDK_DETERMINING_THE_STATUS_OF_A_DEVICE_DBG"></span>


若要显示整个设备树中，启动与根域，使用 **！ devnode 0 1**:

```dbgcmd
kd> !devnode 0 1 
```

标识，而要搜索，可以通过检查驱动程序，或者显示它的总线 devnode。

Devnode 状态标志描述设备的状态。 有关详细信息，请参阅[设备节点状态标志](device-node-status-flags.md)。

在示例中为 **！ devnode**命令，在[调试插件和驱动程序的扩展](extensions-for-debugging-plug-and-play-drivers.md)部分中，swenum 设备已通过即插即用管理器中，因此 DNF\_MADEUP (0x00000001)设置标志。

下面的示例显示了已通过 PCI 总线的设备。 此设备不具有 DNF\_MADEUP 标志设置。

```dbgcmd
0: kd> !devnode 0xfffffa8004483490
DevNode 0xfffffa8004483490 for PDO 0xfffffa800448d060
  Parent 0xfffffa80036766d0   Sibling 0xfffffa8004482010   Child 0xfffffa80058ad720
  InstancePath is "PCI\VEN_8086&DEV_293C&SUBSYS_2819103C&REV_02\3&21436425&0&D7"
  ServiceName is "usbehci"
  State = DeviceNodeStarted (0x308)
  Previous State = DeviceNodeEnumerateCompletion (0x30d)
  StateHistory[09] = DeviceNodeEnumerateCompletion (0x30d)
  StateHistory[08] = DeviceNodeEnumeratePending (0x30c)
  StateHistory[07] = DeviceNodeStarted (0x308)
  StateHistory[06] = DeviceNodeStartPostWork (0x307)
  ...
  Flags (0x6c0000f0)  DNF_ENUMERATED, DNF_IDS_QUERIED, 
                      DNF_HAS_BOOT_CONFIG, DNF_BOOT_CONFIG_RESERVED, 
                      DNF_NO_LOWER_DEVICE_FILTERS, DNF_NO_LOWER_CLASS_FILTERS, 
                      DNF_NO_UPPER_DEVICE_FILTERS, DNF_NO_UPPER_CLASS_FILTERS
  CapabilityFlags (0x00002000)  WakeFromD3
```

**示例**

1. 具有足够的资源的设备 devnode:

```dbgcmd
kd> !devnode 0xff0d06e8 6

DevNode 0xff0d06e8 for PDO 0xff0d07d0 at level 0x3
  Parent 0xff0d1408   Sibling 0000000000   Child 0000000000
  InterfaceType 0xffffffff  Bus Number 0xfffffff0
  InstancePath is "ISAPNP\SUP2171\00000067"
  ServiceName is "Modem"
  TargetDeviceNotify List - f 0xff0d074c  b 0xff0d074c
  Flags (..........)  DNF_PROCESSED, DNF_ENUMERATED,
                      DNF_INSUFFICIENT_RESOURCES, DNF_ADDED,
                      DNF_HAS_BOOT_CONFIG
                      Unknown flags 0x40000000

  IoResList at 0xe133e7a8 : Interface 0x1  Bus 0  Slot 0
    Alternative 0 (Version 1.1)
      Preferred Descriptor 0 - NonArbitrated/ConfigData (0x80) Shared (0x3)
        Flags (0000) -
        Data:              : 0x0 0x61004d 0x680063
      Preferred Descriptor 1 - Port (0x1) Undetermined Sharing (0)
        Flags (0x11) - PORT_IO 16_BIT_DECODE
        0x000008 byte range with alignment 0x000001
        2f8 - 0x2ff
      Preferred Descriptor 2 - Interrupt (0x2) Shared (0x3)
        Flags (0x01) - LATCHED
        0x3 - 0x3
```

请注意，devnode 没有 CM 资源列表中，因为它未启动，并且未使用的资源，尽管它请求的资源。

2. 请注意没有存储在此 devnode 旧驱动程序中的资源。

```dbgcmd
kd> !devnode 0xff0d1648 6

DevNode 0xff0d1648 for PDO 0xff0d22d0 at level 0x2
  Parent 0xff0d2e28   Sibling 0xff0d1588   Child 0000000000
  InterfaceType 0xffffffff  Bus Number 0xffffffff
  InstancePath is "PCI\VEN_102B&DEV_0519\0&60"
  ServiceName is "mga_mil"
  TargetDeviceNotify List - f 0xff0d16ac  b 0xff0d16ac
  Flags (0x6000500b)  DNF_PROCESSED, DNF_STARTED,
                      DNF_ENUMERATED, DNF_ADDED,
                      DNF_LEGACY_DRIVER, DNF_HAS_BOOT_CONFIG
                      Unknown flags 0x40000000
```

您可以检索以下类型的设备的驱动程序的设备对象列表：

```dbgcmd
kd> !drvobj mga_mil

Driver object (ff0bbc10) is for:
 \Driver\mga_mil
Driver Extension List: (id , addr)

Device Object list:
ff0bb900
```

然后可以转储此设备对象的数据：

```dbgcmd
kd> !devobj ff0bb900

Device object (ff0bb900) is for:
 Video0 \Driver\mga_mil DriverObject ff0bbc10
Current Irp 00000000 RefCount 1 Type 00000023 Flags 0000204c
DevExt ff0bb9b8 DevNode ff0bb808
Device queue is not busy.
```

最后，您可以转储 devnode 引用的设备对象。 此 devnode 设备树中未链接。 它表示"伪-devnode"用于声明为旧设备的资源。 请注意 DNF\_资源\_报告标志，指示设备是报告检测到的设备。

```dbgcmd
kd> !devnode ff0bb808 6

DevNode 0xff0bb808 for PDO 0xff0bb900 at level 0xffffffff
  Parent 0xff0daf48   Sibling 0000000000   Child 0000000000
  InterfaceType 0xffffffff  Bus Number 0xffffffff
  TargetDeviceNotify List - f 0xff0bb86c  b 0xff0bb86c
  Flags (0x00000400)  DNF_RESOURCE_REPORTED
  CmResourceList at 0xe12474e8  Version 0.0  Interface 0x5  Bus #0
    Entry 0 - Port (0x1) Shared (0x3)
      Flags (0x01) - PORT_MEMORY PORT_IO
      Range starts at 0x3c0 for 0x10 bytes
    Entry 1 - Port (0x1) Shared (0x3)
      Flags (0x01) - PORT_MEMORY PORT_IO
      Range starts at 0x3d4 for 0x8 bytes
    Entry 2 - Port (0x1) Shared (0x3)
      Flags (0x01) - PORT_MEMORY PORT_IO
      Range starts at 0x3de for 0x2 bytes
    Entry 3 - Memory (0x3) Device Exclusive (0x1)
      Flags (0000) - READ_WRITE
      Range starts at 0x0000000040000000 for 0x4000 bytes
    Entry 4 - Memory (0x3) Device Exclusive (0x1)
      Flags (0000) - READ_WRITE
      Range starts at 0x0000000040800000 for 0x800000 bytes
```

 

 





