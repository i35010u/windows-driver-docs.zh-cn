---
title: 可调整大小 BAR 支持
description: 它是目前典型的离散图形处理单元 (GPU) 能够仅通过 PCI 总线公开其帧缓冲区的一小部分。
ms.assetid: 9CBB8D2E-D3E3-4F52-BCAC-F17446D74991
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4eb377432c7ec01d96d418100244dcaa08545568
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568783"
---
# <a name="resizable-bar-support"></a>可调整大小 BAR 支持


它是目前典型的离散图形处理单元 (GPU) 能够仅通过 PCI 总线公开其帧缓冲区的一小部分。 对于具有 32 位操作系统的兼容性，离散 Gpu 通常声明其帧缓冲区的 256 MB I/O 区域，这是如何典型固件对它们进行配置。

对于 Windows 显示器驱动程序模型 (WDDM) v2，Windows 将会重新协商 GPU 栏 post 固件初始化支持栏，请参阅可调整大小的 Gpu 上的大小[条可调整大小功能](https://go.microsoft.com/fwlink/p/?LinkId=525610)中[PCI SIG 规范库](https://go.microsoft.com/fwlink/p/?LinkId=690603)。

GPU，支持可调整大小栏中，必须确保它可以保留会显示和期间重新编程的栏显示静态图像。 具体而言，我们不希望看到转空白和后端的显示在此过程最多。 请务必已显示的固件映像、 启动加载程序映像和内核模式驱动程序生成的第一个图像之间平滑过渡。 保证重新协商进行时没有 PCI 事务将发生于 GPU。

大多数情况下此重新协商将看不到内核模式驱动程序。 重新协商成功时，内核模式驱动程序将观察 GPU 栏已为其最大大小，以公开分立的 GPU 整个 vram 能够调整大小。

内核模式驱动程序应在成功重设大小，公开单个*CPUVisible*，到视频内存管理器的内存段。 视频内存管理器将 CPU 的虚拟地址直接映射到此范围时 CPU 需要用来访问内存段的内容。

 

 





