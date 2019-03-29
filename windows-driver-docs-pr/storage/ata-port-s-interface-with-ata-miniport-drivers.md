---
title: ATA 端口的可以与 ATA 微型端口驱动程序交互的接口
description: ATA 端口的可以与 ATA 微型端口驱动程序交互的接口
ms.assetid: c3a9b862-8d6e-4ad7-8061-178b053b820c
keywords:
- ATA 端口驱动程序 WDK，微型端口驱动程序
- ATA 微型端口驱动程序 WDK
- 微型端口驱动程序 WDK 存储，ATA 微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6acd4090899140ccc9e8a9b9882bb1efac72434e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567596"
---
# <a name="ata-ports-interface-with-ata-miniport-drivers"></a>ATA 端口的可以与 ATA 微型端口驱动程序交互的接口


## <span id="ddk_ata_ports_interface_with_ata_minport_drivers_kg"></span><span id="DDK_ATA_PORTS_INTERFACE_WITH_ATA_MINPORT_DRIVERS_KG"></span>


**请注意**ATA 端口驱动程序和 ATA 微型端口驱动程序模型可能被修改或不可用在将来。 相反，我们建议使用[Storport 驱动程序](https://msdn.microsoft.com/windows/hardware/drivers/storage/storport-driver)并[Storport 微型端口](https://msdn.microsoft.com/windows/hardware/drivers/storage/storport-miniport-drivers)驱动程序模型。


在 Windows Vista 和更高版本的 Windows 的 IDE 体系结构，有四个系统提供 IDE 驱动程序：

-   ATA 端口驱动程序 (*Ataport.sys*) 的管理控制器通道

-   默认的 ATA 微型端口驱动程序 (*Atapi.sys*)

-   控制器驱动程序 (*Pciidex.sys*)

-   默认控制器微型驱动程序 (*Pciide.sys*)

ATA 端口驱动程序和默认微型端口驱动程序用于 Windows Vista 的新功能。 控制器驱动程序和默认控制器驱动程序不可用于 Windows Vista 的新功能。

在 Microsoft Windows 操作系统版本早于 Windows Vista，供应商可以替换为默认控制器微型驱动程序 (*Pciide.sys*) 使用不同的微型驱动程序的自定义的特定控制器。 有关结构的 Windows 操作系统早于 Windows Vista 中的 IDE 堆栈的详细信息，请参阅[IDE 端口驱动程序](ide-port-driver.md)。

在 Windows Vista 和更高版本的 Windows 将 ATA 端口驱动程序合并到 IDE 体系结构中，供应商可以替换*Pciide.sys*与供应商提供 ATA 微型端口驱动程序。 此驱动程序可以包含多个功能比控制器微型驱动程序。

ATA 微型端口驱动程序可能可以执行两个函数： 它可以充当控制器微型驱动程序和通道微型端口驱动程序通过支持两个接口：

-   控制器接口

    此接口是必需的。 ATA 微型端口驱动程序实现此接口的执行控制器微型驱动程序的功能。 此接口使 ATA 微型端口驱动程序控制的控制器的通道枚举并配置的 IDE 控制器，如计时模式的某些特征。

-   通道接口

    此接口是可选的。 ATA 微型端口驱动程序实现此接口的执行控制器微型驱动程序的函数和通道微型端口驱动程序的函数。 此类驱动程序提供 ATA 端口驱动程序通过挂钩到管理通道 I/O 的微型驱动程序例程。 如果 ATA 微型端口驱动程序不实现此接口，系统将使用默认通道微型端口驱动程序来处理通道操作 (*Atapi.sys*)。

将分离这两个接口符合基础硬件配置，可以提高性能，当通道进行操作以并行，并使微型端口驱动程序代码更轻松地开发和维护。 此外，通过将接口，每个通道都可以有自己的通道微型端口驱动程序，允许端口驱动程序执行操作，如总线重置基于每个通道实例。

下图显示了仅实现控制器接口 ATA 微型端口驱动程序。

![实现控制器接口的供应商微型端口驱动程序](images/ataport1.png)

ATA 微型端口驱动程序初始化控制器接口后，端口驱动程序调用微型端口驱动程序例程，若要配置的控制器中，某些特征，但 ATA 微型端口驱动程序不会处理设备或控制器 I/O。 由 ATA 端口驱动程序和默认通道微型端口驱动程序处理所有 I/O 请求。

在大多数情况下，无需实现这种类型的供应商微型驱动程序。 默认控制器微型驱动程序 (*Pciide.sys*) 是不足以管理大多数控制器硬件。

下图显示了在其中供应商提供的微型端口驱动程序函数同时作为通道驱动程序和控制器驱动程序的配置。

![供应商微型端口驱动程序实现控制器和通道接口](images/ataport2.png)

ATA 微型端口驱动程序实现通道接口公开到控制器驱动程序的控制器和通道管理例程 (*Pciidex.sys*)。 出于性能原因*Pciidex.sys*传递通道管理条目指向 ATA 端口驱动程序，以及 ATA 端口驱动程序调用 ATA 微型端口驱动程序的通道管理例程中介不直接*Pciidex.sys*。 *Pciidex.sys*驱动程序调用 ATA 微型端口驱动程序的控制器例程。

 

 


