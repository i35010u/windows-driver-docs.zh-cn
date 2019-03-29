---
title: 支持符合多功能标准的电脑卡
description: 支持符合多功能标准的电脑卡
ms.assetid: 1ab295b6-42c9-46fc-97e0-2228e189ff37
keywords:
- PCMCIA 总线 WDK 多功能设备
- mf.inf
- 硬件 Id WDK 多功能设备
- 子函数硬件 Id WDK 多功能设备
- 系统提供多功能总线驱动程序 WDK
- mf.sys
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecb53e8bceeb05b58c0bd6c9e901cfd414ea4aa0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575989"
---
# <a name="supporting-pc-cards-that-conform-to-the-multifunction-standard"></a>支持符合多功能标准的电脑卡





如果 16 位 ISA 样式 PC 卡设备完全实现 PC 卡多功能标准，并且是否正确，在基于 NT 的平台上的此类设备的供应商可以依赖于以下的系统提供组件，以处理的软件方面多功能语义：

-   多功能设备 INF 文件。 （系统提供）

    PCMCIA 总线驱动程序指定要使用系统提供多功能 INF 文件 (mf.inf) 来配置设备的配置管理器将导致该设备的硬件 ID。 Mf.inf 文件指定的类"多功能"和其关联的 GUID （如在 devguid.h 中定义）。

-   多功能设备的函数驱动程序。 （系统提供）

    Mf.inf 文件指定为设备功能驱动程序的系统提供多功能总线驱动程序 (mf.sys)。

    Mf.sys 总线驱动程序枚举设备的功能。 PCMCIA 总线驱动程序读取来确定每个函数的资源要求在设备上配置注册表。

    请参阅[使用 System-Supplied 多功能总线驱动程序](using-the-system-supplied-multifunction-bus-driver.md)有关使用系统提供 mf.sys 驱动程序详细信息。

多功能符合标准的 PC 卡设备的供应商必须提供以下支持各个功能：

-   每个函数的设备的即插即用功能驱动程序。 （供应商提供）

    由于多功能总线驱动程序处理的多功能语义，功能的驱动程序可以是相同的驱动程序，可在函数已打包为单个设备。

-   用于设备的每个函数的 INF 文件。 （供应商提供）

    INF 文件可以是可在函数已打包为单个设备的相同文件。 INF 文件不需要任何特殊的多功能语义。

### <a name="child-function-hardware-ids-created-by-the-pcmcia-bus-driver"></a>PCMCIA 总线驱动程序创建的子函数的硬件 Id

对于 true 多功能 PC 卡设备 PCMCIA 总线驱动程序，以及 mf.sys，将创建的子函数的硬件 Id。 这些 Id 具有以下格式：

```cpp
    <Manufacturer-name>-<Product-ID-string>-DEV<number>-CRC
```

按以下格式&lt;*数*&gt;是该函数的从零开始编号。

例如，PCMCIA 总线驱动程序创建子函数硬件 Id，如下所示：

```cpp
    3COM_Corporation-3C562D/3C563D-DEV0-4893
    3COM_Corporation-3C562D/3C563D-DEV1-4893
```

多功能 PC 卡设备的子函数的 INF 文件必须指定 PCMCIA 总线驱动程序和 mf.sys 报告的硬件 ID。

 

 




