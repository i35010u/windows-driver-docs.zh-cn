---
title: 可调整大小 BAR 支持
description: 通常，对于离散图形处理单元而言， (GPU) 只在 PCI 总线上暴露一小部分帧缓冲区。
ms.assetid: 9CBB8D2E-D3E3-4F52-BCAC-F17446D74991
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e45cf89c30963c37a70c3f4fca2c39f13da9274
ms.sourcegitcommit: abe7fe9f3fbee8d12641433eeab623a4148ffed3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "92185215"
---
# <a name="resizable-bar-support"></a>可调整大小 BAR 支持

通常，对于离散图形处理单元而言， (GPU) 只在 PCI 总线上暴露一小部分帧缓冲区。 为了与32位操作系统兼容，离散 Gpu 通常会为其帧缓冲区声明 256MB i/o 区域，这是典型固件配置它们的方式。

对于 Windows 显示器驱动程序模型 (WDDM) v2，Windows 将重新协商 GPU 栏的大小在支持可调整大小栏的 Gpu 上进行固件初始化，请参阅 [PCI SIG 规范库](https://go.microsoft.com/fwlink/p/?LinkId=690603)中的可调整大小的 bar 功能。

GPU （支持可调整大小的条）必须确保在 reprogramming 时，它可以保持显示并显示静态图像。 特别是，我们不希望在此过程中看到显示为空白并进行备份。 在显示的固件、启动加载程序映像和第一个内核模式驱动程序生成的映像之间进行平滑过渡非常重要。 在重新协商时，保证不会向 GPU 发出 PCI 事务。

大多数情况下，这种重新协商对于内核模式驱动程序不可见。 重新协商成功后，内核模式驱动程序会观察到 GPU 栏已调整到最大大小，以公开离散 GPU 的整个 VRAM。

调整成功后，内核模式驱动程序应向视频内存管理器公开单一的 *CPUVisible*内存段。 当 CPU 需要访问内存段的内容时，视频内存管理器会将 CPU 虚拟地址直接映射到此范围。
