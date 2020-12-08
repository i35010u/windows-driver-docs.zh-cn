---
title: 时钟和链接位置寄存器
description: 时钟和链接位置寄存器
keywords:
- 时钟注册 WDK 音频
- 链接位置注册 WDK 音频
- HD 音频，墙壁时钟寄存器
- 高清晰音频 (HD 音频) ，墙壁时钟寄存器
- HD 音频，链接位置寄存器
- 高清晰音频 (HD 音频) ，链接位置寄存器
- 时钟 WDK 音频，HD 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81e805e011480b228fb68080cd3d7c5a5b656cb3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798809"
---
# <a name="wall-clock-and-link-position-registers"></a>时钟和链接位置寄存器


HD 音频控制器包含32位时钟计数器寄存器，它以 HD 音频链路的位时钟速率为增量，每89秒翻转一次。 通过测量设备硬件时钟之间的相对偏差，软件使用此计数器在两个或更多控制器设备之间进行同步。

此外，HD 音频控制器还包含一组链接位置寄存器。 每个 DMA 引擎都有一个链接位置注册，指示引擎通过 HD 音频链接传输的数据的当前读取或写入位置。 位置寄存器将当前位置表示为相对于循环缓冲区开始的字节偏移量：

-   在呈现流中，链接位置寄存器指示 DMA 引擎将通过指向编解码器的链接发送的下一个字节的循环缓冲区偏移量。

-   在捕获流中，链接位置寄存器指示 DMA 引擎将通过链接从编解码器接收的下一个字节的循环缓冲区偏移量。

循环缓冲区偏移量只是循环缓冲区开始处当前读取或写入位置的偏移量（以字节为单位）。 到达缓冲区的末尾后，位置将环绕到缓冲区的开头，并且循环缓冲区偏移量将重置为零。 循环缓冲区驻留在系统内存中。 有关详细信息，请参阅 [INTEL HD 音频](https://www.intel.com/content/www/us/en/standards/intel-standards-and-initiatives.html)网站上的 *Intel 高质音频规范*。

内核模式功能驱动程序可以直接读取墙壁时钟和链接位置寄存器。 若要启用直接访问，HD 音频总线驱动程序会将包含寄存器的物理内存映射到系统虚拟内存。 函数驱动程序调用 [**GetWallClockRegister**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_wall_clock_register) 或 [**GetLinkPositionRegister**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_link_position_register) 例程，以获取指向时钟寄存器或链接位置寄存器的系统虚拟地址指针。 这两个例程在高清音频 DDI 的两个版本中均可用。

HD 音频控制器硬件镜像墙壁时钟，并将链接位置寄存器连接到不包含控制器中任何其他寄存器的内存页。 因此，如果函数驱动程序将镜像的墙壁时钟或位置寄存器映射到用户模式，则任何用户模式程序都不能访问任何其他控制器的注册。 驱动程序永远不允许用户模式程序接触到其他寄存器，并对硬件进行编程。

注册镜像必须容纳主机处理器的页面大小。 典型页面大小可能是4096或8192字节，具体取决于主机处理器的体系结构。

 

