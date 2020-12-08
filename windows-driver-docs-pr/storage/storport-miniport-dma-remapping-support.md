---
title: Storport 微型端口驱动程序中的 DMA 重映射支持
description: Storport 微型端口驱动程序中的 DMA 重映射支持
ms.date: 07/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: 3a906b8f7168eb02c588a3e3efe356783ff3614d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834939"
---
# <a name="dma-remapping-support-in-storport-miniport-drivers"></a>Storport 微型端口驱动程序中的 DMA 重映射支持

[StorAhci storport 微型端口驱动程序](https://github.com/microsoft/Windows-driver-samples/tree/master/storage/miniports/storahci)示例代码演示了如何在 Storport 微型端口驱动程序中支持 DMA 重新映射。 有关 DMA 重新映射和内核 DMA 保护的其他信息，请参阅 [为设备驱动程序启用 DMA 重映射](../pci/enabling-dma-remapping-for-device-drivers.md)。

> [!NOTE]
>
> 对于 Storport 微型端口驱动程序， [验证是否为特定的设备驱动程序实例启用](../pci/enabling-dma-remapping-for-device-drivers.md#validating-that-dma-remapping-is-enabled-for-a-specific-device-driver-instance) 了 "dma 重新映射策略" 设备属性的默认值对于 windows 10 版本1803和1809，以及2个适用于 windows 10 版本1903及更高版本。

此属性对应于 [**DEVPKEY_Device_DmaRemappingPolicy**](../install/devpkey-device-dmaremappingpolicy.md)。
