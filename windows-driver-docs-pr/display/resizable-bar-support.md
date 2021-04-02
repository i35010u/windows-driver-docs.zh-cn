---
title: 可调整大小的栏的系统和驱动程序支持
description: OS 和驱动程序支持可调整大小的条形
ms.date: 03/30/2021
ms.localizationpriority: medium
ms.custom: contperf-fy21q3
ms.openlocfilehash: 55bcc5d2e1368241a9906d9741f5681461d664f3
ms.sourcegitcommit: 38feaa2a1d3495eb20ccf846eb9cbcd67e8ae4ec
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2021
ms.locfileid: "106099065"
---
# <a name="system-and-driver-support-for-resizable-bar"></a>可调整大小的栏的系统和驱动程序支持

通常，对于离散图形处理单元而言， (GPU) 只在 PCI 总线上暴露一小部分帧缓冲区。 为了与32位操作系统兼容，离散 Gpu 通常会为其帧缓冲区声明 256 MB 的 i/o 区域，这是典型固件配置它们的方式。

在支持可调整大小的基址寄存器 (BAR) 的 Gpu 上，Windows 将在 Windows 显示驱动程序模型中的固件初始化之后重新协商 GPU 栏的大小 (WDDM) v2 和更高版本。 有关可调整大小的栏的详细信息，请参阅 [PCI SIG 规范库](https://go.microsoft.com/fwlink/p/?LinkId=690603)中的可调整大小的 bar 功能规范。

支持可调整大小的栏的 GPU 必须确保在 reprogramming 时可以保持显示并显示静态图像。 在此过程中，显示不应为空白，也不应备份。 在固件显示的图像、启动加载程序映像和内核模式驱动程序生成的第一个映像之间进行平滑过渡非常重要。 请注意，协商正在进行时，不会向 GPU 发出 PCI 事务。

这种重新协商在内核模式驱动程序中是不可见的。 重新协商成功后，内核模式驱动程序会观察到 GPU 栏已调整到最大大小，以公开离散 GPU 的整个 VRAM。

调整成功后，内核模式驱动程序应向视频内存管理器公开单个 [*CPUVisible*](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentflags) 内存段。 当 CPU 需要访问内存段的内容时，视频内存管理器会将 CPU 虚拟地址直接映射到此范围。
