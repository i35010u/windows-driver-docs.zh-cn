---
title: 使用 AVStream 将视频捕获到 VRAM
description: 使用 AVStream 将视频捕获到 VRAM
keywords:
- AVStream WDK，VRAM 捕获
- VRAM 捕获 WDK AVStream
- 将视频捕获到 VRAM WDK AVStream
- 视频捕获到 VRAM WDK AVStream
- 音频捕获到 VRAM WDK AVStream
- 数据捕获到 VRAM WDK AVStream
- 显示微型驱动程序 WDK VRAM 捕获
- 微型驱动程序 WDK VRAM 捕获
ms.date: 06/16/2020
ms.localizationpriority: medium
ms.openlocfilehash: dd38a5bff850dd99667e242aef2098893d28560c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839363"
---
# <a name="capturing-video-to-vram-using-avstream"></a>使用 AVStream 将视频捕获到 VRAM

从 Windows Vista 开始，AVStream 驱动程序可以直接将视频和音频捕获到图形适配器的 VRAM 中。 在 Windows Vista 之前存在的 AVStream 驱动程序必须先将数据置于 VRAM 中，将其传输到系统内存，最后返回 VRAM 才能显示。

VRAM 捕获支持利用 Windows 显示驱动程序模型提供的 GPU 计划和 VRAM 虚拟化 [ (WDDM) 设计指南](../display/windows-vista-display-driver-model-design-guide.md)。

若要捕获到 VRAM，设备必须在同一视频卡上包含捕获和显示功能。

以下部分介绍如何将 VRAM 捕获支持添加到新的或现有的驱动程序：

[AVStream 中的 VRAM 捕获概述](overview-of-vram-capture-in-avstream.md)

[VRAM 捕获属性](vram-capture-properties.md)

[将未压缩的数据捕获到 VRAM](capturing-uncompressed-data-to-vram.md)

[将 VRAM 捕获支持添加到现有的 AVStream 驱动程序](adding-vram-capture-support-to-existing-avstream-drivers.md)

可以在 [AVStream 模拟硬件示例驱动程序 (AVSHwS) ](/samples/microsoft/windows-driver-samples/avstream-simulated-hardware-sample-driver-avshws/)中找到显示 VRAM 捕获的示例代码。
