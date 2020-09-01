---
title: ATA 端口的可以与 ATA 微型端口驱动程序交互的接口
description: ATA 端口的可以与 ATA 微型端口驱动程序交互的接口
ms.assetid: c3a9b862-8d6e-4ad7-8061-178b053b820c
keywords:
- ATA 端口驱动程序 WDK、微型端口驱动程序
- ATA 微型端口驱动程序 WDK
- 微型端口驱动程序 WDK 存储，ATA 微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9907f690cbabb8c024b5825864fab692050c7ff
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192435"
---
# <a name="ata-ports-interface-with-ata-miniport-drivers"></a>ATA 端口的可以与 ATA 微型端口驱动程序交互的接口


## <span id="ddk_ata_ports_interface_with_ata_minport_drivers_kg"></span><span id="DDK_ATA_PORTS_INTERFACE_WITH_ATA_MINPORT_DRIVERS_KG"></span>


**注意** ATA 端口驱动程序和 ATA 微型端口驱动程序模型可能会在将来更改或不可用。 相反，我们建议使用 [storport 驱动](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver) 程序和 [storport 微型端口](./storport-miniport-drivers.md) 驱动程序模型。


在 Windows Vista 和更高版本的 Windows 的 IDE 体系结构中，有四个系统提供的 IDE 驱动程序：

-   ATA 端口驱动程序 (管理控制器通道 *Ataport.sys*) 

-   默认 ATA 微型端口驱动程序 (*Atapi.sys*) 

-   控制器驱动程序 (*Pciidex.sys*) 

-   默认控制器微型驱动程序 (*Pciide.sys*) 

ATA 端口驱动程序和默认的微型端口驱动程序是适用于 Windows Vista 的新驱动程序。 控制器驱动程序和默认控制器驱动程序并非适用于 Windows Vista。

在早于 Windows Vista 的 Microsoft Windows 操作系统版本中，供应商可以将默认控制器微型驱动程序 (*Pciide.sys*) 替换为特定控制器自定义的其他微型驱动程序。 有关 windows Vista 之前的 Windows 操作系统中 IDE 堆栈的结构的详细信息，请参阅 [Ide 端口驱动程序](ide-port-driver.md)。

在 Windows Vista 和更高版本的 Windows 中，将 ATA 端口驱动程序合并到 IDE 体系结构中时，供应商可以将 *Pciide.sys* 替换为供应商提供的 ATA 小型端口驱动程序。 此驱动程序可包含比控制器微型驱动程序更多的功能。

ATA 微型端口驱动程序可能会执行两个功能：它可以同时充当控制器微型驱动程序和通道微型端口驱动程序，同时支持两个接口：

-   控制器接口

    此接口是必需的。 实现此接口的 ATA 微型端口驱动程序执行控制器微型驱动程序的功能。 此接口使 ATA 微型端口驱动程序能够控制控制器通道的枚举，并配置 IDE 控制器的某些特性（例如计时模式）。

-   通道接口

    此接口是可选的。 实现此接口的 ATA 微型端口驱动程序同时执行控制器微型驱动程序和通道微型端口驱动程序的功能。 此类驱动程序将 ATA 端口驱动程序与挂钩一起提供给管理通道 i/o 的微型驱动程序例程。 如果 ATA 微型端口驱动程序未实现此接口，系统将使用默认通道微型端口驱动程序来处理 (*Atapi.sys*) 的通道操作。

分离这两个接口符合基础硬件配置，可在并行操作通道时提高性能，并使微型端口驱动程序代码更易于开发和维护。 而且，通过分隔接口，每个通道都可以有自己的通道微型端口驱动程序的实例，使端口驱动程序能够按照每个通道的频率执行操作，如总线重置。

下图显示了仅实现控制器接口的 ATA 微型端口驱动程序。

![用于实现控制器接口的供应商微型端口驱动程序](images/ataport1.png)

ATA 微型端口驱动程序初始化控制器接口后，端口驱动程序会调用微型端口驱动程序例程来配置控制器的某些特征，但 ATA 微型端口驱动程序不会处理设备或控制器 i/o。 所有 i/o 请求均由 ATA 端口驱动程序和默认通道微型端口驱动程序处理。

在大多数情况下，您不必实现此类供应商微型驱动程序。 默认的控制器微型驱动程序 (*Pciide.sys*) 足以管理大多数控制器硬件。

下图显示了供应商提供的微型端口驱动程序在中充当通道驱动程序和控制器驱动程序的配置。

![同时实现控制器和通道接口的供应商微型端口驱动程序](images/ataport2.png)

实现通道接口的 ATA 微型端口驱动程序向控制器驱动程序公开控制器和通道管理例程， (*Pciidex.sys*) 。 出于性能方面的原因， *Pciidex.sys* 将通道管理入口点传递给 ata 端口驱动程序，ata 端口驱动程序会直接调用 ata 微型端口驱动程序的通道管理例程，而不会 *Pciidex.sys*的中介。 *Pciidex.sys*驱动程序调用 ATA 微型端口驱动程序的控制器例程。

 

