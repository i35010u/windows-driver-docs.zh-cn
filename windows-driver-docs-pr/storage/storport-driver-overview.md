---
title: Storport 驱动程序
description: Storport 驱动程序
ms.assetid: d5bda2f6-c4bb-4b90-a149-131785295687
keywords:
- 存储端口驱动程序 WDK、Storport 驱动程序
- Storport 驱动程序 WDK
- Storport 驱动程序 WDK，关于 Storport 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3e1f63499a162258ecb089f1ac6455e043013c3
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606525"
---
# <a name="storport-driver"></a>Storport 驱动程序

除了 SCSI 端口驱动程序以外，Microsoft Windows Server 2003 和更高版本还提供 Storport （*storport*），这是一个特别适用于高性能总线（如光纤通道总线和 RAID 适配器）的存储端口驱动程序。

使用 Storport （而非 SCSI 端口驱动程序）有以下几个优点：

- 提高了性能，包括吞吐量和使用的系统资源。

- 提高了微型端口驱动程序接口，可满足高端存储供应商的需求，尤其是基于主机的 RAID 和光纤通道供应商。

建议所有供应商尽可能使用 Storport，而不是 SCSI 端口驱动程序。 但会应用某些限制。 Storport 不能与不支持即插即用的适配器或设备一起使用。 所有 DMA 设备都必须具有总线控制 DMA 功能，因为 Storport 不支持程控 i/o 或从属模式 DMA。 其他限制适用于标记队列、autorequest 感知、WMI 支持、设备必须报告的 SCSI 查询数据的种类以及直接从适配器的 ROM BIOS 启动的情况。 有关使用 Storport 驱动程序的详细限制列表，请参阅对[适配器使用 storport 的要求](requirements-for-using-storport-with-an-adapter.md)。

为了更好地利用供应商在 SCSI 端口微型端口驱动程序中所做的投资，Storport 遵循 SCSI 端口-微型端口驱动程序体系结构，只需进行很少的修改。 对 SCSI 端口驱动程序接口的更改是在新算法能够产生可度量的速度增加的区域中进行的，或者是需要为高速总线添加支持的位置。
