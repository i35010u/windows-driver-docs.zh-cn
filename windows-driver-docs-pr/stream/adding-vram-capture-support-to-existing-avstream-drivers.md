---
title: 将 VRAM 捕获支持添加到现有的 AVStream 驱动程序
description: 将 VRAM 捕获支持添加到现有的 AVStream 驱动程序
ms.assetid: 10736533-3873-4f1d-91c5-d2e55163daaa
keywords:
- VRAM 捕获 WDK AVStream，现有驱动程序支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79c68b415af97e7cdf5b28bf5eeca5470094c131
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845584"
---
# <a name="adding-vram-capture-support-to-existing-avstream-drivers"></a>将 VRAM 捕获支持添加到现有的 AVStream 驱动程序


若要将 VRAM 捕获支持添加到使用 DMA 的现有以引脚为中心的 AVStream 驱动程序，请执行以下步骤。

1.  将 VRAM 捕获支持添加到[*AVStrMiniPinProcess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspin)回调例程。 [AVStream 模拟硬件示例驱动程序（AVSHwS）](https://go.microsoft.com/fwlink/p/?linkid=256083)的 CCapturePin： r*方法中的* **:P：**

2.  如本部分前面所述，处理 VRAM 捕获属性请求。

3.  在子捕获驱动程序或父显示微型端口驱动程序中添加支持，以将 DX 内核句柄映射到 VRAM 地址。

4.  实现 StopCapture 功能。 当 KMD 发送 stop 捕获通知时，捕获驱动程序必须停止所有捕获。 为了注册通知，捕获驱动程序提供了一个[*DxgkDdiStopCapture*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_stopcapture)回调例程。 捕获驱动程序在收到此通知后，将无法从用户模式发出任何捕获请求。

 

 




