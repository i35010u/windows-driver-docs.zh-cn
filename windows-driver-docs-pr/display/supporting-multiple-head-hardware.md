---
title: 支持多头硬件
description: 支持多头硬件
keywords:
- 多头硬件 WDK DirectX 9。0
- 硬件多头支持 WDK DirectX 9。0
- 多头硬件 WDK DirectX 9.0，关于多头硬件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1ec16f1f7a466b7cf4d531cb83524ba1ad98d61
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793845"
---
# <a name="supporting-multiple-head-hardware"></a>支持多头硬件


## <span id="ddk_supporting_multiple_head_hardware_gg"></span><span id="DDK_SUPPORTING_MULTIPLE_HEAD_HARDWARE_GG"></span>


DirectX 9.0 版本驱动程序可以为多头卡实现多头支持，其中包含以下功能：

-   适用于所有显示设备的通用帧缓冲区和快捷键 (卡上) 。

-   独立数字到模拟转换器 (DAC) 并监视每个显示设备 (head) 的输出。

-   比异类显示卡数量更多的可用多监视器支持。

-   一个 head 控件或独立操作。 单个设备可公开给一个应用程序，并且该设备可以驱动多个全屏交换链。 因此，所有资源都由多个磁头共享，并且每个头的功能完全相同。 每个 head 都可以设置为独立的显示模式;然后，应用程序可以在不同时间对每个 head 调用 **当前** 方法。 标头的每个交换链都必须为全屏。 设备进入多头模式后，必须保持为全屏模式。 过渡回到开窗模式需要销毁设备 (除了最小化操作) 。

请注意，对于 DirectX 8.1 及更早版本的应用程序，DirectX 9.0 驱动程序仍应使用以前的一种机制，该机制将视频内存分割到打印头，并将每个机头视为完全独立的加速器。 仅当应用程序在 DirectX 9.0 多头模式下进行了编码时，驱动程序才能使用这些新的多头功能。 当在两种操作模式间切换时，将通知该驱动程序。

以下部分介绍了驱动程序如何支持多头硬件。

[识别适配器组和提供功能](identifying-adapter-group-and-providing-capabilities.md)

[创建头](creating-heads.md)

[句柄分配示例](example-of-handle-assignments.md)

[管理多头内存](managing-multiple-head-memory.md)

[报告多头视频内存](reporting-multiple-head-video-memory.md)

[使用多个头进行呈现](presentation-with-multiple-heads.md)

[使用多个多头适配器](using-multiple-multiple-head-adapters.md)

 

 





