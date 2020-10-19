---
title: PDEV 初始化和清理
description: PDEV 初始化和清理
ms.assetid: 26651869-861a-4be8-bc6c-df3704ca714e
keywords:
- 绘制 WDK GDI，初始化，PDEV 初始化
- 初始化图形驱动程序 WDK Windows 2000 显示，PDEV
- GDI WDK Windows 2000 显示，初始化，PDEV
- 图形驱动程序 WDK Windows 2000 显示、初始化、PDEV
- PDEV WDK GDI
- DrvEnablePDEV
- 绘制 WDK GDI，PDEV 清理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 411539b4ab39e68724653074a0cc54eb8918c6bb
ms.sourcegitcommit: abe7fe9f3fbee8d12641433eeab623a4148ffed3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "92185158"
---
# <a name="pdev-initialization-and-cleanup"></a>PDEV 初始化和清理

每个内核模式显卡驱动程序都表示由 GDI 管理的单个逻辑设备。 反过来，驱动程序可以管理一个或多个 *PDEV* 结构。 PDEV 是物理设备的逻辑表示形式。 它的特点是可以支持的硬件、逻辑地址和曲面的类型：

- **硬件类型**：作为驱动程序的一个示例，该驱动程序支持硬件类型所述的 PDEV，一个驱动程序可以支持 LaserWhiz、LaserWhiz II 和 LaserWhiz 超级打印机。 GDI 传递的设备名称指定从支持驱动程序的设备总数中请求的逻辑设备。

- **逻辑地址**：单个驱动程序可以支持连接到 LPT1、COM2 的打印机和名为 \\ \\ SERVER1 PSLASER 的服务器 \\ ，例如。 此外，可以同时支持多个 VGA 显示的显示驱动程序可以通过端口号来区分它们，如0x3CE、0x2CE 等。 打印机的逻辑地址和其他硬复制输出设备由 GDI 确定; [**EngWritePrinter**](/windows/win32/api/winddi/nf-winddi-engwriteprinter) 函数将输出定向到适当的目标。 显示可以隐式确定其自己的逻辑地址，也可以从 [**DEVMODEW**](/windows/win32/api/wingdi/ns-wingdi-devmodew)的 private 部分中检索该地址。

  DEVMODEW 结构为驱动程序提供所需的环境设置，例如设备的名称和特定于打印机或显示驱动程序的其他信息。

- **曲面**：每个 PDEV 都需要一个独特的图面。 例如，如果打印机驱动程序同时处理两个打印作业，每个打印作业都需要不同的页面格式，如横向和纵向格式，则每个打印作业都需要不同的 PDEV。 同样，显示驱动程序可以在同一显示器上支持两个桌面，每个桌面需要不同的 PDEV 和表面。 对于每个所需的图面，都有一个对 [**DrvEnablePDEV**](/windows/win32/api/winddi/nf-winddi-drvenablepdev) 函数的调用，可以为该表面创建不同的 PDEV。

为响应对 *DrvEnablePDEV*的调用，驱动程序会通过几个结构将有关硬件设备功能的信息返回到 GDI。

在 GDI 调用*DrvEnablePDEV*之前， [**GDIINFO**](/windows/win32/api/winddi/ns-winddi-gdiinfo)结构为零填充。 驱动程序会在 GDIINFO 中填入以下信息，以将以下信息传达给 GDI：

- 驱动程序版本号
- 基本设备技术 (光栅与矢量
- 可打印页面的大小和分辨率
- 调色板和灰色缩放信息
- 字体和文本功能
- 半色调支持
- 样式步骤号

驱动程序只应填写它支持的字段，而忽略其余字段。

驱动程序将用说明此 PDEV 的图形功能的标志填充 [**lnk-devinfo**](/windows/win32/api/winddi/ns-winddi-devinfo) 结构。 几乎在所有情况下，来自 LNK-DEVINFO 的信息都会告诉 GDI 驱动程序可以提供的图形支持级别。 例如，如果需要使用高音 clef，则 LNK-DEVINFO 中的信息会告知 GDI 驱动程序是否可以处理贝塞尔曲线，或是否改为发送多个行段。 驱动程序应填写所支持的任意数目的字段，并保持其他字段不变。

驱动程序必须提供的另一条重要信息是 (*phsurfPatterns*) 指针写入缓冲区，该缓冲区使用表示标准填充模式的图面填充。 除了标准填充模式， *phsurfPatterns* 可以包含 null，这会导致 GDI 根据设备分辨率和像素大小自动创建模式图面。 当在上调用 GDI 以使用标准模式 [实现画笔](realizing-brushes.md) 时，它将调用 [**DrvRealizeBrush**](/windows/win32/api/winddi/nf-winddi-drvrealizebrush) 函数来实现为所请求的模式定义的画笔。

对于支持设备的内核驱动程序，GDI 将 [**DrvEnablePDEV**](/windows/win32/api/winddi/nf-winddi-drvenablepdev) 为 *hDriver*。 对于打印机驱动程序， *hDriver* 提供了打印机的句柄，并用于对后台处理程序的调用（如 **EngWritePrinter**）。

当 GDI 调用 *DrvEnablePDEV*时，驱动程序必须分配支持创建的 PDEV 所需的内存，即使调用 *DrvEnablePDEV* 来为不同模式创建其他 PDEV 结构。  (驱动程序可以有多个活动的 PDEVs，但一次只能启用一个。 ) 不过，在 GDI 调用 [**DrvEnableSurface**](/windows/win32/api/winddi/nf-winddi-drvenablesurface)之前不支持实际的表面。

如果设备图面需要分配位图，则不需要进行分配，除非在 [**DrvEnableSurface**](/windows/win32/api/winddi/nf-winddi-drvenablesurface) 函数) 中通常 (启用了该图面。 尽管应用程序通常会在实际写入设备之前请求设备信息，但等待分配大位图可以节省宝贵的资源并提高系统初始化期间的驱动程序性能。

PDEV 安装完成后，GDI 会调用 [**DrvCompletePDEV**](/windows/win32/api/winddi/nf-winddi-drvcompletepdev) 函数来通知驱动程序安装物理设备已完成。 此函数还为驱动程序提供了 PDEV 的 GDI 逻辑句柄，驱动程序将在调用 GDI 函数时使用该驱动程序。

对驱动程序的 [**DrvDisablePDEV**](/windows/win32/api/winddi/nf-winddi-drvdisablepdev) 函数的调用指示不再需要给定的物理设备。 在此函数中，驱动程序应释放物理设备使用的任何内存和资源。

另请参阅 [启用和禁用图面](enabling-and-disabling-the-surface.md)。
