---
title: 访问的帧缓冲区和硬件注册
description: 访问的帧缓冲区和硬件注册
ms.assetid: 6f735f33-0bb7-45b8-ac01-f34ec4937a8b
keywords:
- 显示帧缓冲区 WDK Windows 2000
- 缩小显示驱动程序 WDK Windows 2000
- 大小 WDK Windows 2000 的屏幕
- 显示驱动程序 WDK Windows 2000，减小大小
- 视频硬件注册 WDK Windows 2000 显示
- 硬件注册 WDK Windows 2000 显示
- 银行 WDK Windows 2000 显示
- 存款的内存 WDK Windows 2000 时，显示
- 显示线性帧缓冲区 WDK Windows 2000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88f2f3a3282b0b255fe592142232c5388ea7ef36
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541192"
---
# <a name="accessing-the-frame-buffer-and-hardware-registers"></a>访问的帧缓冲区和硬件注册


## <span id="ddk_accessing_the_frame_buffer_and_hardware_registers_gg"></span><span id="DDK_ACCESSING_THE_FRAME_BUFFER_AND_HARDWARE_REGISTERS_GG"></span>


有几种方法来减少显示驱动程序大小。 例如，您可以实现仅这些函数显示驱动程序，可以执行速度快于 GDI，，然后指定 GDI 执行其他操作。 GDI 通常执行绘制到大量*线性帧缓冲区*以减少驱动程序的大小。 无法访问 GDI*累积的积分内存*直接; 因此，无法以线性方式可寻址帧缓冲区时，显示器驱动程序，必须为一系列的划分帧缓冲区*银行*，并为 GDI 提供一种方法若要执行到相应的银行其描述的操作。 请参阅[支持累积的积分帧缓冲区](supporting-banked-frame-buffers.md)有关详细信息。

显示驱动程序可以直接访问 O 映射和内存映射视频寄存器。 此访问权限使显示驱动程序以实现高性能。 例如，驱动程序可能需要访问视频硬件寄存器将线条图形命令发送以高吞吐量。

同样，对于图形卡，如 S3，许多中的图形引擎代码最里面的循环，需要读取和写入多个视频控制器端口 （例如，在图形模式、 位块传输和线条图形中的文本输出）。 不要求显示驱动程序将 IOCTL 发送到每个请求的微型端口驱动程序，而是显示驱动程序允许直接访问视频硬件。

 

 





