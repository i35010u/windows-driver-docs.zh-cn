---
title: PDEV 初始化和清理
description: PDEV 初始化和清理
ms.assetid: 26651869-861a-4be8-bc6c-df3704ca714e
keywords:
- 绘制 WDK GDI，初始化、 PDEV 初始化
- 初始化的图形显示驱动程序 WDK Windows 2000，PDEV
- GDI WDK Windows 2000 显示中，将进行初始化，PDEV
- 图形驱动程序 WDK Windows 2000 显示，请初始化 PDEV
- PDEV WDK GDI
- DrvEnablePDEV
- 绘制 WDK GDI，PDEV 清理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2cfa4b833895a1a420b93116e7c0ec1e516235d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524209"
---
# <a name="pdev-initialization-and-cleanup"></a>PDEV 初始化和清理


## <span id="ddk_pdev_initialization_and_cleanup_gg"></span><span id="DDK_PDEV_INITIALIZATION_AND_CLEANUP_GG"></span>


每个内核模式图形驱动程序表示通过 GDI 管理的单个逻辑设备。 反过来，驱动程序可以管理一个或多个*PDEV*结构。 PDEV 是物理设备的逻辑表示形式。 其特征是硬件、 逻辑地址和图面，可以支持的类型：

-   **类型的硬件**âˆ 作为支持的硬件类型特征 PDEV 驱动程序的示例，一个驱动程序可能支持 LaserWhiz、 LaserWhiz II 和 LaserWhiz 超级打印机。 通过 GDI 传递的设备名称指定的驱动程序支持的设备的总集请求的逻辑设备。

-   **逻辑地址**âˆ 单个驱动程序可以支持附加到 LPT1、 COM2 和一个名为服务器的打印机\\ \\SERVER1\\PSLASER，例如。 此外，可以支持多个同时显示 VGA 显示器驱动程序可能区分它们的端口号，例如 0x3CE，0x2CE，依次类推。 打印机的逻辑地址和其他硬拷贝输出设备确定通过 GDI;[ **EngWritePrinter** ](https://msdn.microsoft.com/library/windows/hardware/ff565467)函数将输出定向到正确的目的地。 显示可以隐式确定其自己的逻辑地址或地址检索的专用部分[ **DEVMODEW**](https://msdn.microsoft.com/library/windows/hardware/ff552837)。

    DEVMODEW 结构提供了驱动程序和必需的环境设置，例如设备和其他特定于打印机或显示器驱动程序的信息的名称。

-   **图面**âˆ 每个 PDEV 需要唯一的图面。 例如，如果打印机驱动程序将同时用于两个打印作业，每个要求的不同页格式的横向和纵向格式，如每个打印作业需要不同 PDEV。 同样，显示器驱动程序可能支持在相同的显示，每个桌面需要不同的 PDEV 和图面上的两个台式机。 对于所需的每个图面上，没有调用[ **DrvEnablePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff556211)函数来创建该图面不同 PDEV。

中的调用的响应*DrvEnablePDEV*，驱动程序返回到 GDI 通过几种结构的硬件设备的功能信息。

[ **GDIINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff566484)结构为零填充 GDI 调用之前*DrvEnablePDEV*。 该驱动程序填充 GDIINFO 通信到 GDI 的以下信息：

-   驱动程序的版本号

-   基本设备技术 （光栅图与矢量）

-   大小和分辨率的可打印页面

-   调色板颜色和灰度级信息

-   字体和文本的功能

-   半色调支持

-   样式步骤数

该驱动程序应填充它支持字段，而忽略其余。

该驱动程序会填写[ **DEVINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff552835)结构描述此 PDEV 的图形功能标志。 在几乎所有情况下，从 DEVINFO 信息告知 GDI 的驱动程序可以提供的图形支持级别。 例如，如果需要绘制的高音谱号，则 DEVINFO 内的信息告知 GDI 驱动程序是否可以处理贝塞尔曲线或 GDI 是否必须改为发送多个直线线段。 该驱动程序应填充它支持的所有字段，并将其他内容保持不变。

该驱动程序必须提供的信息的另一个重要部分是一个指针 (*phsurfPatterns*) 使用句柄对于图面表示标准的填充模式填充的缓冲区。 除了标准的填充模式中， *phsurfPatterns*可以包含 null，这会导致 GDI 创建自动根据设备分辨率和像素大小的模式图面。 当 GDI 调用到[意识到画笔](realizing-brushes.md)使用标准模式时，它将调用[ **DrvRealizeBrush** ](https://msdn.microsoft.com/library/windows/hardware/ff556273)函数来实现请求的模式为定义的画笔。

GDI 传递[ **DrvEnablePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff556211)句柄*hDriver*，支持设备的内核驱动程序。 打印机驱动程序， *hDriver*提供到打印机的句柄，用于在调用中，如**EngWritePrinter**，到后台处理程序。

每当调用 GDI *DrvEnablePDEV*，该驱动程序必须分配支持 PDEV 创建时，所需的内存即使*DrvEnablePDEV*调用来创建不同的模式下其他 PDEV 结构. （驱动程序有多个活动 PDEVs，但只有一个可以启用一次。）但是，实际表面不支持 GDI 调用[ **DrvEnableSurface**](https://msdn.microsoft.com/library/windows/hardware/ff556214)。

如果设备界面需要的位图的分配，分配则不需要启用面之前 (通常在[ **DrvEnableSurface** ](https://msdn.microsoft.com/library/windows/hardware/ff556214)函数)。 尽管应用程序通常请求实际写入到设备之前，设备信息，正在等待分配一个大位图可以节省宝贵的资源并提高在系统初始化过程中的驱动程序性能。

PDEV 安装完成后，调用 GDI [ **DrvCompletePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff556181)函数来通知该驱动程序的物理设备的安装已完成。 此函数为 PDEV，驱动程序使用对 GDI 函数的调用中，还提供了与 GDI 的逻辑句柄的驱动程序。

驱动程序的调用[ **DrvDisablePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff556198)函数指示不再需要给定的物理设备。 在此函数中，驱动程序应释放任何内存和物理设备使用的资源。

请参考[启用和禁用在图面](enabling-and-disabling-the-surface.md)。

 

 





