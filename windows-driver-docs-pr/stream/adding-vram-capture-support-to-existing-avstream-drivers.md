---
title: 将 VRAM 捕获支持添加到现有的 AVStream 驱动程序
description: 将 VRAM 捕获支持添加到现有的 AVStream 驱动程序
ms.assetid: 10736533-3873-4f1d-91c5-d2e55163daaa
keywords:
- Vram 能够捕获 WDK AVStream，现有的驱动程序支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 127d5be369e571c275097b275168acba8792fbe7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386776"
---
# <a name="adding-vram-capture-support-to-existing-avstream-drivers"></a>将 VRAM 捕获支持添加到现有的 AVStream 驱动程序


若要添加到现有 pin 构建以 AVStream 驱动程序使用 DMA 的 vram 能够捕获支持，请执行以下步骤。

1.  添加到的 vram 能够捕获支持你[ *AVStrMiniPinProcess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspin)回调例程。 **CCapturePin::Process**中的方法*Capture.cpp*的[AVStream 模拟硬件示例驱动程序 (AVSHwS)](https://go.microsoft.com/fwlink/p/?linkid=256083)演示一种方法执行此操作。

2.  处理 vram 能够捕获属性请求如在本部分中前面所述。

3.  在子捕获驱动程序或父显示微型端口驱动程序将 DX 内核句柄映射到 vram 能够地址中添加支持。

4.  实现 StopCapture 功能。 当 KMD 发送停止捕获通知时，捕获驱动程序必须停止所有捕获。 若要注册通知，捕获驱动程序提供了[ *DxgkDdiStopCapture* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_stopcapture)回调例程。 捕获驱动程序应该会收到此通知后来自用户模式下的任何捕获请求失败。

 

 




