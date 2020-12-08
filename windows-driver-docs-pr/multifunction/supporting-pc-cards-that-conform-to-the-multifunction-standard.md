---
title: 支持符合多功能标准的电脑卡
description: 支持符合多功能标准的电脑卡
keywords:
- PCMCIA 总线 WDK 多功能设备
- mf.inf
- 硬件 Id WDK 多功能设备
- 子函数硬件 Id WDK 多功能设备
- 系统提供的多功能总线驱动程序 WDK
- mf.sys
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26d68255eb4ab274e7e9d67521f180f663621f67
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825567"
---
# <a name="supporting-pc-cards-that-conform-to-the-multifunction-standard"></a>支持符合多功能标准的电脑卡





如果16位 ISA 样式的 PC 卡设备完全和正确地实现了 PC 卡多功能标准版，则基于 NT 的平台上此类设备的供应商可以依赖于以下系统提供的组件来处理多功能语义的软件方面：

-   多功能设备的 INF 文件。  (系统提供的) 

    PCMCIA 总线驱动程序为设备指定硬件 ID，使 configuration manager 能够使用系统提供的多功能 INF 文件 (mf) 来配置设备。 Mf 文件指定类 "多功能" 及其关联的 GUID (在 devguid) 中定义。

-   多功能设备的函数驱动程序。  (系统提供的) 

    Mf .inf 文件指定系统提供的多功能总线驱动程序 ( # A0) 作为设备的函数驱动程序。

    mf.sys 总线驱动程序枚举设备的功能。 PCMCIA 总线驱动程序读取设备上的配置寄存器，以确定每个函数的资源要求。

    有关使用系统提供的 mf.sys 驱动程序的详细信息，请参阅 [使用 System-Supplied 多功能总线驱动程序](using-the-system-supplied-multifunction-bus-driver.md) 。

符合标准的多功能 PC 卡设备供应商必须为单个功能提供以下支持：

-   设备的每个功能的 PnP 函数驱动程序。  (供应商提供的) 

    由于多功能总线驱动程序处理多功能语义，因此函数驱动程序可以是在将函数打包为单个设备时使用的相同驱动程序。

-   设备的每个功能的 INF 文件。  (供应商提供的) 

    如果将这些文件打包为单独的设备，则 INF 文件可以是使用的相同文件。 INF 文件不需要任何特殊的多功能语义。

### <a name="child-function-hardware-ids-created-by-the-pcmcia-bus-driver"></a>PCMCIA 总线驱动程序创建的子函数硬件 Id

对于真正的多功能 PC 卡设备，PCMCIA 总线驱动程序与 mf.sys 一起为子函数创建硬件 Id。 这些 Id 的格式如下：

```cpp
    <Manufacturer-name>-<Product-ID-string>-DEV<number>-CRC
```

在此格式中， &lt; *number* &gt; 是函数的从零开始的编号。

例如，PCMCIA 总线驱动程序创建子函数硬件 Id，如下所示：

```cpp
    3COM_Corporation-3C562D/3C563D-DEV0-4893
    3COM_Corporation-3C562D/3C563D-DEV1-4893
```

多功能 PC 卡设备的子功能的 INF 文件必须指定 PCMCIA 总线驱动程序报告的硬件 ID 并 mf.sys。

 

 




