---
title: 支持多个头硬件
description: 支持多个头硬件
ms.assetid: ea618586-3649-405c-b1fd-78a11f14c742
keywords:
- 多个头硬件 WDK DirectX 9.0
- 硬件多磁头支持 WDK DirectX 9.0
- 有关多个头硬件的多个头硬件 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5df8008ccbb6c650498d92ef55e6fb54798a88b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542141"
---
# <a name="supporting-multiple-head-hardware"></a>支持多个头硬件


## <span id="ddk_supporting_multiple_head_hardware_gg"></span><span id="DDK_SUPPORTING_MULTIPLE_HEAD_HARDWARE_GG"></span>


DirectX 9.0 版本驱动程序可以实现对多个头卡具有以下功能的多个头支持：

-   常见的帧缓冲区和所有加速器在卡片上显示设备 （头）。

-   独立于数字模拟转换器 (DAC) 和监视输出的每个显示设备 (head)。

-   更多可用多监视器支持比类似数量的异类显示卡。

-   一个头控件或独立的操作。 可以向应用程序公开的单个设备，该设备可以推动几个全屏交换链。 因此，共享所有资源是很多头，并且每个有相同的功能。 可以将每个头设置为独立的显示模式;然后，应用程序可以调用**存在**方法在不同时间每个标头。 Head 每个交换链必须全屏幕。 一旦设备进入多头模式，则必须始终保持全屏。 转换为窗口模式要求的设备 （除了最小化操作） 的析构。

请注意，对于 DirectX 8.1 和早期的应用程序，DirectX 9.0 驱动程序应仍使用除以头之间的视频内存和每个头视为完全独立的加速器的以前的机制。 如果应用程序编码为多个头在 DirectX 9.0 中正常工作模式的作用只驱动程序将使用这些新的多个 head 功能。 该驱动程序收到通知时两种操作模式之间进行切换。

以下部分介绍如何驱动程序支持多个头硬件。

[标识适配器组，并提供功能](identifying-adapter-group-and-providing-capabilities.md)

[创建头](creating-heads.md)

[句柄分配示例](example-of-handle-assignments.md)

[管理多个头的内存](managing-multiple-head-memory.md)

[报告多个头视频内存](reporting-multiple-head-video-memory.md)

[通过多个磁头的演示文稿](presentation-with-multiple-heads.md)

[使用多个多头适配器](using-multiple-multiple-head-adapters.md)

 

 





