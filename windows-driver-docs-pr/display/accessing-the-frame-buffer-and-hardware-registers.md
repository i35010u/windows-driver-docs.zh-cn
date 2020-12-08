---
title: 访问帧缓冲区和硬件寄存器
description: 访问帧缓冲区和硬件寄存器
keywords:
- 帧缓冲区 WDK Windows 2000 显示
- 减小显示器驱动程序大小 WDK Windows 2000
- size WDK Windows 2000 显示
- 显示驱动程序 WDK Windows 2000，减小大小
- 视频硬件注册 WDK Windows 2000 显示器
- 硬件注册 WDK Windows 2000 显示器
- 银行 WDK Windows 2000 显示器
- 存款 memory WDK Windows 2000 显示
- 线性帧缓冲 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18d12ec80b4321f8878a22f5301484f17b5ba007
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810565"
---
# <a name="accessing-the-frame-buffer-and-hardware-registers"></a>访问帧缓冲区和硬件寄存器


## <span id="ddk_accessing_the_frame_buffer_and_hardware_registers_gg"></span><span id="DDK_ACCESSING_THE_FRAME_BUFFER_AND_HARDWARE_REGISTERS_GG"></span>


可以通过多种方式来减小显示器驱动程序的大小。 例如，您只能实现显示驱动程序执行速度比 GDI 更快的那些函数，然后指定 GDI 来执行所有其他操作。 GDI 通常会执行大量的绘图到 *线性帧缓冲区* 来减小驱动程序的大小。 GDI 无法直接访问 *存款内存* ;因此，当帧缓冲区不可线性寻址时，显示驱动程序必须将帧缓冲区划分为一系列的 *银行* ，并为 GDI 提供一种向相应银行执行其绘制操作的方法。 有关详细信息，请参阅 [支持存款帧缓冲区](supporting-banked-frame-buffers.md) 。

显示驱动程序可以直接访问 i/o 映射和内存映射视频寄存器。 此访问权限允许显示驱动程序实现高性能。 例如，驱动程序可能需要访问视频硬件寄存器以高吞吐量发送行绘制命令。

同样，对于诸如 S3 的图形卡，图形引擎代码中的许多最内层的循环都需要读取和写入多个视频控制器端口 (例如，在图形模式下的文本输出、位块传输和线条绘制) 。 不需要显示驱动程序即可将 IOCTL 发送到每个请求的微型端口驱动程序，而是允许显示驱动程序直接访问视频硬件。

 

 





