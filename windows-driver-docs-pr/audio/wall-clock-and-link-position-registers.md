---
title: 时钟和链接位置寄存器
description: 时钟和链接位置寄存器
ms.assetid: 6764affc-a4f0-4568-aa27-7f12e86b818b
keywords:
- 时钟注册 WDK 音频
- 链接位置注册 WDK 音频
- HD Audio 时钟注册
- 高清晰度音频 (HD Audio)、 时钟注册
- HD Audio，链接位置注册
- 高清晰度音频 (HD Audio) 链接位置寄存器
- 时钟 WDK 音频，HD Audio
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af329930b41058ec8ca10abae347fdf5c27ba5e8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544731"
---
# <a name="wall-clock-and-link-position-registers"></a>时钟和链接位置寄存器


HD Audio 控制器包含 32 位墙时钟计数器寄存器的 HD 音频链接并将回滚位时钟速率大约每隔 89 秒递增。 软件使用此计数器来测量设备的硬件时钟之间的相对偏移的两个或多个控制器设备之间进行同步。

此外，HD Audio 控制器包含链接位置寄存器的组。 每个 DMA 引擎提供的链接放置寄存器，该值指示当前的读取或写入该引擎通过 HD 音频链接传输数据的位置。 位置注册表达循环缓冲区的当前位置为从一开始的字节偏移量：

-   在呈现流中，链接位置注册指示 DMA 引擎将通过编解码器的链接发送的下一个字节的循环缓冲区偏移量。

-   在捕获流中，链接位置注册指示 DMA 引擎通过该链接将接收来自编解码器的下一个字节的循环缓冲区偏移量。

循环缓冲区偏移量为只是以字节为单位的当前读取或写入的位置开始从循环缓冲区的偏移量。 一旦达到缓冲区的末尾，位置回绕到缓冲区和循环缓冲区偏移量重置为零的开始。 循环缓冲区驻留在系统内存中。 有关详细信息，请参阅*Intel 高定义音频规范*处[Intel HD Audio](https://go.microsoft.com/fwlink/p/?linkid=42508)网站。

内核模式功能驱动程序可以读取时钟和直接链接位置寄存器。 若要启用直接访问，HD Audio 总线驱动程序映射包含到系统虚拟内存的寄存器的物理内存。 该函数将驱动程序调用[ **GetWallClockRegister** ](https://msdn.microsoft.com/library/windows/hardware/ff536401)或[ **GetLinkPositionRegister** ](https://msdn.microsoft.com/library/windows/hardware/ff536398)例程，以获取虚拟系统到墙上时钟注册或链接位置注册的地址指针。 HD 音频 DDI 这两个版本中提供了两个例程。

HD Audio 控制器硬件镜像到不包含任何控制器中的其他寄存器的内存页的墙时钟和链接位置寄存器。 因此，如果功能驱动程序映射的镜像的时钟或注册到用户模式下，任何用户模式程序可以访问的控制器的任何位置的其他寄存器。 该驱动程序永远不会允许用户模式程序触摸这些其他寄存器和计划硬件。

注册镜像必须适应主机处理器的页面大小。 根据主机处理器体系结构，典型的页面大小可能是 4,096 或 8192 个字节。

 

 




