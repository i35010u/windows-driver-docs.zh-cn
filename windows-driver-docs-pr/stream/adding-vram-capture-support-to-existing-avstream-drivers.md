---
title: 将 VRAM 捕获支持添加到现有的 AVStream 驱动程序
description: 将 VRAM 捕获支持添加到现有的 AVStream 驱动程序
keywords:
- VRAM 捕获 WDK AVStream，现有驱动程序支持
ms.date: 06/15/2020
ms.localizationpriority: medium
ms.openlocfilehash: 89d602719d42fe951032e8f0ebfb26be3704115f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792563"
---
# <a name="adding-vram-capture-support-to-existing-avstream-drivers"></a>将 VRAM 捕获支持添加到现有的 AVStream 驱动程序

若要将 VRAM 捕获支持添加到使用 DMA 的现有以引脚为中心的 AVStream 驱动程序，请执行以下步骤。

1. 将 VRAM 捕获支持添加到 [*AVStrMiniPinProcess*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspin) 回调例程。 [AVStream 模拟硬件示例驱动程序 () AVSHwS](/samples/microsoft/windows-driver-samples/avstream-simulated-hardware-sample-driver-avshws/)中的 **CCapturePin：:P r** 方法会显示一种执行 *此操作的* 方法。

1. 如本部分前面所述，处理 VRAM 捕获属性请求。

1. 在子捕获驱动程序或父显示微型端口驱动程序中添加支持，以将 DX 内核句柄映射到 VRAM 地址。

1. 实现 StopCapture 功能。 当 KMD 发送 stop 捕获通知时，捕获驱动程序必须停止所有捕获。 为了注册通知，捕获驱动程序提供了一个 [*DxgkDdiStopCapture*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_stopcapture) 回调例程。 捕获驱动程序在收到此通知后，将无法从用户模式发出任何捕获请求。
