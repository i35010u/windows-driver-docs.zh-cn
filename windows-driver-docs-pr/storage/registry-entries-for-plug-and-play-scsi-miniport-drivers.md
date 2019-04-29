---
title: 即插即用 SCSI 微型端口驱动程序的注册表项
description: 即插即用 SCSI 微型端口驱动程序的注册表项
ms.assetid: d4c7c8ee-9d04-4fd4-9b70-2630d2ce6401
keywords:
- SCSI 微型端口驱动程序 WDK 存储，即插即用
- 即插即用 WDK SCSI
- Plug and Play WDK SCSI
- PnPInterface
- 注册表 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03afdab59d1a54b7d24f137405ffc2b1785e4ac9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366244"
---
# <a name="registry-entries-for-plug-and-play-scsi-miniport-drivers"></a>即插即用 SCSI 微型端口驱动程序的注册表项


## <span id="ddk_registry_entries_for_plug_and_play_scsi_miniport_drivers_kg"></span><span id="DDK_REGISTRY_ENTRIES_FOR_PLUG_AND_PLAY_SCSI_MINIPORT_DRIVERS_KG"></span>


若要支持插，SCSI 微型端口驱动程序必须：

-   安装作为 HBA 的服务。

-   具有**PnPInterface**指示的接口的注册表项对于该微型端口驱动程序支持插。

安装微型端口驱动程序作为 SCSI HBA 的服务通常通过提供正确的驱动程序为一个给定的 HBA 来控制该设备插硬件 ID 相匹配的安装程序信息 (INF) 文件。 有关设置的 INF 文件的详细信息，请参阅[插](https://msdn.microsoft.com/library/windows/hardware/ff547125)*。*

除非微型端口驱动程序安装为服务的 HBA **PnPInterface**注册表项会*防止*中初始化的微型端口驱动程序。 仅当插查找相应的 HBA 时初始化的指定的接口。 如果没有服务正确地分配到 HBA，插将永远不会确定要通知时检测到设备的驱动程序。 此行为是有意设计和微型端口驱动程序不应尝试绕过它。

**PnPInterface**注册表项应建立**服务**微型端口驱动程序的密钥。 例如，以下注册表项启用插调用因为虚构的微型端口驱动程序。

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

值前面 REG\_dword 值对应于该接口\_类型的枚举类型中声明*miniport.h*。 此示例中的值指示因为微型端口驱动程序支持以下接口插：**PCIBus** (5)， **Isa** (1)， **Eisa** （2） 和**PCMCIABus** (8)。 以下注册表值\_DWORD 是一个标志，指示插支持接口。 （目前，此标志可以是任何值，但必须存在。 在将来，该标志可能是可选的。）

之后**PnPInterface**值在注册表中设置和重新启动系统，微型端口驱动程序可以初始化为插驱动程序。 在初始化期间，SCSI 端口驱动程序检查注册表，以确定是否应为插或旧版的驱动程序运行微型端口驱动程序。 SCSI 端口驱动程序会检查注册表中的微型端口驱动程序支持 （例如，PCI 和 ISA） 每个接口类型。 这主要用于简化调试多个接口微型端口驱动程序的编写器。 微型端口驱动程序编写器应确保微型端口驱动程序是支持所有的插驱动程序接口该驱动程序正在运行的支持。

 

 




