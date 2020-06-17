---
title: 使用 AVStream 将视频捕获到 VRAM
description: 使用 AVStream 将视频捕获到 VRAM
ms.assetid: c4ca4a67-83cb-4a89-bc84-e06b1dc67b66
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
ms.openlocfilehash: a10245f7caf2f989ea6804882a259841cd2debd5
ms.sourcegitcommit: 97a8d24b1b48602e4ccaa63a113f7c8cdb0c6df5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2020
ms.locfileid: "84812445"
---
# <a name="capturing-video-to-vram-using-avstream"></a>使用 AVStream 将视频捕获到 VRAM

从 Windows Vista 开始，AVStream 驱动程序可以直接将视频和音频捕获到图形适配器的 VRAM 中。 在 Windows Vista 之前存在的 AVStream 驱动程序必须先将数据置于 VRAM 中，将其传输到系统内存，最后返回 VRAM 才能显示。

VRAM 捕获支持利用[Windows 显示驱动程序模型（WDDM）设计指南](https://docs.microsoft.com/windows-hardware/drivers/display/windows-vista-display-driver-model-design-guide)提供的 GPU 计划和 VRAM 虚拟化。

若要捕获到 VRAM，设备必须在同一视频卡上包含捕获和显示功能。

以下部分介绍如何将 VRAM 捕获支持添加到新的或现有的驱动程序：

[AVStream 中的 VRAM 捕获概述](overview-of-vram-capture-in-avstream.md)

[VRAM 捕获属性](vram-capture-properties.md)

[将未压缩的数据捕获到 VRAM](capturing-uncompressed-data-to-vram.md)

[将 VRAM 捕获支持添加到现有的 AVStream 驱动程序](adding-vram-capture-support-to-existing-avstream-drivers.md)

可以在[AVStream 模拟硬件示例驱动程序（AVSHwS）](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/avstream-simulated-hardware-sample-driver-avshws/)中找到显示 VRAM 捕获的示例代码。
