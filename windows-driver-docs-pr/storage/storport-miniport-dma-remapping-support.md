---
title: Storport 微型端口驱动程序中的 DMA 重映射支持
description: Storport 微型端口驱动程序中的 DMA 重映射支持
ms.assetid: 9d1e1549-8b11-4a9a-b068-7b1d75c58e52
ms.date: 07/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: 7e28d0708fd2927bd26f050a03a2a6b392aee3c1
ms.sourcegitcommit: 1ab8fc6d15fac78ce243f3852d86733ebfca40dc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2020
ms.locfileid: "86436879"
---
# <a name="dma-remapping-support-in-storport-miniport-drivers"></a>Storport 微型端口驱动程序中的 DMA 重映射支持

[StorAhci storport 微型端口驱动程序](https://github.com/microsoft/Windows-driver-samples/tree/master/storage/miniports/storahci)示例代码演示了如何在 Storport 微型端口驱动程序中支持 DMA 重新映射。 有关 DMA 重新映射和内核 DMA 保护的其他信息，请参阅[为设备驱动程序启用 DMA 重映射](https://docs.microsoft.com/windows-hardware/drivers/pci/enabling-dma-remapping-for-device-drivers)。

> [!NOTE]
>
> 对于 Storport 微型端口驱动程序，[验证是否为特定的设备驱动程序实例启用](https://docs.microsoft.com/windows-hardware/drivers/pci/enabling-dma-remapping-for-device-drivers#validating-that-dma-remapping-is-enabled-for-a-specific-device-driver-instance)了 "dma 重新映射策略" 设备属性的默认值对于 windows 10 版本1803和1809，以及2个适用于 windows 10 版本1903及更高版本。

此属性对应于[**DEVPKEY_Device_DmaRemappingPolicy**](../install/devpkey-device-dmaremappingpolicy.md)。
