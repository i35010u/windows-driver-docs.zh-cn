---
title: 即插即用 SCSI 微型端口驱动程序的注册表项
description: 即插即用 SCSI 微型端口驱动程序的注册表项
ms.assetid: d4c7c8ee-9d04-4fd4-9b70-2630d2ce6401
keywords:
- SCSI 微型端口驱动程序 WDK 存储，PnP
- PnP WDK SCSI
- 即插即用 WDK SCSI
- PnPInterface
- 注册表 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63016f2a6791d453ad369c46963f7e20b8155496
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733721"
---
# <a name="registry-entries-for-plug-and-play-scsi-miniport-drivers"></a>即插即用 SCSI 微型端口驱动程序的注册表项


## <span id="ddk_registry_entries_for_plug_and_play_scsi_miniport_drivers_kg"></span><span id="DDK_REGISTRY_ENTRIES_FOR_PLUG_AND_PLAY_SCSI_MINIPORT_DRIVERS_KG"></span>


若要支持即插即用，SCSI 微型端口驱动程序必须：

-   将作为服务安装到 HBA。

-   注册表中有一个 **PnPInterface** 条目，指示微型端口驱动程序支持即插即用的接口。

为 SCSI HBA 安装微型端口驱动程序的方法通常是通过将给定 HBA 的即插即用硬件 ID 与给定 HBA 的硬件 ID 相匹配的安装信息 (INF) 文件来控制该设备。 有关设置 INF 文件的详细信息，请参阅 [即插即用](../kernel/introduction-to-plug-and-play.md)*。*

除非已将微型端口驱动程序安装为 HBA 的服务，否则 **PnPInterface** 注册表项将 *阻止* 小型端口驱动程序初始化。 仅当即插即用查找适当的 HBA 时，才会初始化指定的接口。 如果没有任何服务正确分配给 HBA，即插即用将永远不会确定在检测到设备时要通知的驱动程序。 此行为是设计使然，而微型端口驱动程序不应尝试绕过它。

**PnPInterface**注册表项应在微型端口驱动程序的 "**服务**" 项下进行。 例如，以下注册表项启用了名为 Twiddle 的虚构微型端口驱动程序的即插即用。

```cpp
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services
    \Twiddle
        \Parameters
            \PnpInterface
                5 : REG_DWORD : 1
                1 : REG_DWORD : 1
                2 : REG_DWORD : 1
                8 : REG_DWORD : 1
```

REG DWORD 前面的值 \_ 对应于 \_ 在 *微型端口 .h*中声明的接口类型枚举类型。 本示例中的值指示 Twiddle 微型端口驱动程序支持以下接口的即插即用： **PCIBus** (5) 、 **Isa** (1) 、 **Eisa** (2) 和 **PCMCIABus** (8) 。 注册表 DWORD 后面的值 \_ 是一个标志，用于指示接口即插即用支持。  (当前，此标志可以是任何值，但必须存在。 将来，标志可能是可选的。 ) 

在注册表中设置 **PnPInterface** 值并重新启动系统后，可将微型端口驱动程序初始化为即插即用驱动程序。 在初始化期间，SCSI 端口驱动程序会检查注册表，以确定是否应将微型端口驱动程序作为即插即用或旧驱动程序运行。 SCSI 端口驱动程序检查注册表中是否存在微型端口驱动程序支持的每个接口类型 (例如，PCI 和 ISA) 。 这主要用于简化多接口小型端口驱动程序的编写器调试。 微型端口驱动程序编写器应确保微型端口驱动程序能够作为驱动程序支持的所有接口的即插即用驱动程序运行。

 

