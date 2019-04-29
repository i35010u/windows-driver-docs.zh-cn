---
title: 初始化和调用 IDE 微型驱动程序例程
description: 初始化和调用 IDE 微型驱动程序例程
ms.assetid: ae7b19a9-0a2e-4231-b008-879b7f6c8566
keywords:
- IDE 控制器微型驱动程序 WDK 存储初始化
- 存储 IDE 控制器微型驱动程序 WDK，初始化
- IDE 控制器微型驱动程序 WDK 存储中，使用调用
- 存储 IDE 控制器微型驱动程序 WDK 中，使用调用
- 初始化 IDE 控制器微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cce0d2261f3eb302904f5ead51ed0217bf97a411
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359110"
---
# <a name="initializing-and-calling-ide-minidriver-routines"></a>初始化和调用 IDE 微型驱动程序例程


## <span id="ddk_initializing_and_calling_ide_minidriver_routines_kr"></span><span id="DDK_INITIALIZING_AND_CALLING_IDE_MINIDRIVER_ROUTINES_KR"></span>


所有 IDE 控制器微型驱动程序必须都提供一系列的标准例程的实现特定于硬件的功能。 下图说明了如何 IDE 控制器微型驱动程序使其例程可供控制器驱动程序。 请注意，PciIdeX 库，但从概念上独立于 IDE 控制器驱动程序，该图中所示包含在控制器驱动程序的可执行文件中， *pciidex.sys*。 当微型驱动程序调用 PciIdeX 库例程时，它实际上调用例程在控制器驱动程序中。

![微型驱动程序例程初始化程序流](images/idecallbacks.png)

1.  PnP 管理器加载 IDE 控制器驱动程序的微型驱动程序，然后调用其[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程，它将指针传递到控制器驱动程序的驱动程序对象。

2.  微型驱动程序的**DriverEntry**调用[ **PciIdeXInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff563788)库例程，它将指针传递给微型驱动程序的**GetControllerProperties**例程。

3.  **PciIdeXInitialize**存储到指针**GetControllerProperties**驱动程序对象中。

4.  PnP 管理器调度 IRP\_MN\_启动\_到 IDE 控制器驱动程序的设备请求启动控制器。 IDE 控制器驱动程序将收到的请求中其[ **DispatchPnP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程并调用一个内部例程的启动设备。

5.  控制器驱动程序会检索一个指向**GetControllerProperties**存储在驱动程序对象。

6.  控制器驱动程序调用**GetControllerProperties**，并向其传递一个指向[ **IDE\_控制器\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff559076)结构。

7.  **GetControllerProperties**加载到 IDE 的一组标准的微型驱动程序例程的指针\_控制器\_属性。

一旦微型驱动程序使用 IDE 来填充\_控制器\_属性结构使用指向微型驱动程序的例程的函数指针，该控制器驱动程序可以调用它们。

每个微型驱动程序必须为要调用的控制器提供的例程如下所示：

此例程确定是否启用指定的通道。

此例程将报告 IDE 控制器硬件的属性。

此例程该值指示是否可以在一次访问其控制器的两个通道。

此例程返回最佳 PIO 模式和最佳的 DMA 模式为每个设备所示*XferMode*。

此例程指示这超直接内存访问 (UDMA) 传输模式是最新和最好的设备。

此例程确定是否可以通过 DMA I/O。

[**HwIdeXChannelEnabled**](https://msdn.microsoft.com/library/windows/hardware/ff557252)

[**HwIdeXGetControllerProperties**](https://msdn.microsoft.com/library/windows/hardware/ff557254)

[**HwIdeXSyncAccessRequired**](https://msdn.microsoft.com/library/windows/hardware/ff557256)

[**HwIdeXTransferModeSelect**](https://msdn.microsoft.com/library/windows/hardware/ff557260)

[**HwIdeXUdmaModesSupported**](https://msdn.microsoft.com/library/windows/hardware/ff557264)

[**HwIdeXUseDma**](https://msdn.microsoft.com/library/windows/hardware/ff557266)

 

 




