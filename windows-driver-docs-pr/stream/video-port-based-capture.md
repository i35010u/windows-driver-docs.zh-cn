---
title: 基于视频端口的捕获
description: 基于视频端口的捕获
keywords:
- 筛选器关系图配置 WDK 视频捕获、基于视频端口的捕获
- 基于视频端口的捕获 WDK 视频捕获
- 视频端口引脚 WDK 视频捕获
- VPEs WDK 视频捕获
- 视频端口扩展 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f085216f129f084c09d286b5c7bd8cd5f4e4091f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792081"
---
# <a name="video-port-based-capture"></a>基于视频端口的捕获


捕获基于视频端口的设备必须提供连接到视频端口管理器的视频端口 pin。 视频端口 pin 允许基于硬件的传输显示预览流，而无需 CPU 或外围组件互连 (PCI) 总线开销。 单独的 pin 提供捕获功能 (例如，必须将捕获的视频写入磁盘) 。 在捕获过程中，会向显示驱动程序提供捕获缓冲区，该驱动程序会通过总线主控来填充缓冲区。 本部分稍后和 [内核模式视频传输](../display/kernel-mode-video-transport.md)中进一步详细介绍了捕获微型驱动程序和显示驱动程序之间的交互。

在运行 Microsoft Windows 98 SE 或 Windows 2000 的系统上，覆盖混音器筛选器 (更高版本的操作系统中的视频端口管理器筛选器) 不支持辅助监视器上的视频端口连接。 在这种情况下，pin 连接会失败。 辅助监视器上的视频端口连接在运行 Windows Millennium Edition (Windows Me) 和 Windows XP 的系统上受支持。

如果设备支持 VBI 捕获，则它通常会公开另外两个 pin： VPVBI 和 VBI。 视频端口管理器筛选器使用 VPVBI pin 为 VBI 捕获分配视频端口图面。 VBI pin 本身提供原始 VBI 示例。

下图显示了 VPVBI 和 VBI 捕获的单独路径。

![演示 vpvbi 和 vbi 捕获的单独路径的示意图](images/video-port-capture.gif)

特定于此类筛选器关系图的属性集是 [KSPROPSETID \_ VPCONFIG 和 KSPROPSETID \_ VPVBIConfig](./kspropsetid-vpconfig-and-kspropsetid-vpvbiconfig.md) and [PROPSETID \_ 分配器 \_ 控件](./propsetid-allocator-control.md)。

### <a name="using-the-video-port-extensions-vpes"></a>使用视频端口扩展 (VPEs) 

**注意：** 以下各段仅适用于 Windows Vista 的下一个版本之前的操作系统。 如果显示驱动程序使用新的 Windows Vista 驱动程序显示模型 (LDDM) ，则将在 Windows Vista 中禁用 VPE。

视频捕获微型驱动程序可以使用 [**DxApi**](/windows-hardware/drivers/ddi/dxapi/nf-dxapi-dxapi) 函数与视频微型端口驱动程序通信，以允许捕获流式处理视频，使其在捕获硬件和显示硬件之间通过视频端口总线传输。 流包含 NTSC、PAL 或 SECAM 视频的顺序字段，还可以包括 (VBI) 和时间码 (横向同步和垂直同步) 数据。 视频流特征（包括维度、颜色格式、频率、缩放和裁剪）通过 VPE DirectDraw 接口在用户模式下进行配置。 开始流式处理后，会在内核模式下调用 **DxApi** 以捕获各个帧。 为了支持显示更改，如分辨率更改或切换到或从全屏命令提示符切换，视频捕获微型驱动程序还必须向视频微型端口驱动程序注册，以便它们能够响应此类显示更改事件。

VPEs 和 **DxApi** 函数已引入到带有 DirectX 5.0 的 DirectDraw DDI。 Windows 2000 及更高版本的操作系统中的视频微型端口驱动程序支持 **DxApi** 。 虚拟显示微型端口驱动程序 (miniVDD) 在 Windows 98 和 Windows Me 操作系统中支持 **DxApi** 。 若要使用 **DxApi** 启用内核模式视频传输，WDM 视频捕获微型驱动程序必须包含 *ddkmapi* (DirectDraw 内核模式 API) 头文件并链接到 *DxApi* 库。 **DxApi** 库使用 *dxapi.sys* 导出的功能。 仅当已加载 DirectDraw 时， *DxApi.sys* 才可用，因为 **DxApi** 是 VPEs 的一部分。

**DxApi** 是 *DxApi.sys* 公开的单个内核模式 API。 视频端口扩展是 *DDraw.dll* 公开的用户模式 API。 视频捕获微型驱动程序必须对 **DxApi** 进行几个不同的调用，以设置和配置视频端口硬件，使其正确流式传输。

**DxApi** 是封装多个函数标识符的单个函数。 微型驱动程序将第一个参数中所需的函数标识符传递给 **DxApi**。 **DxApi** 的其余参数适用于对应于函数标识符和缓冲区长度的结构的微型驱动程序分配缓冲区。 函数的行为以及输入和输出缓冲区的大小和格式取决于指定的函数标识符。 [DxApi 函数和标识符](/windows-hardware/drivers/ddi/index)中介绍了此行为。

WDK 提供两个示例驱动程序，用于演示如何实现 **DxApi** 功能。 ATIWDM 示例需要特定硬件才能运行。 TestCap 示例不需要硬件，并适用于所有平台。 可以使用 GraphEdt 工具与其中一个示例进行交互。

视频捕获微型驱动程序必须调用 **DxApi** 来执行的常见功能如下：

-   打开内核模式 DirectDraw (**DxApi** 函数标识符设置为 DD \_ DxApi OPENDIRECTDRAW) 的句柄 \_ 。 此操作必须在 IRQL = 被动级别执行 \_ 。

-   获取硬件视频端口的内核模式功能 (将 **DxApi** 函数标识符设置为 DD \_ DxApi \_ GETKERNELCAPS) 。

-   注册回调以处理 DirectDraw 事件，如 mode 切换为全屏命令提示符 (**DxApi** 函数标识符设置为 DD \_ DxApi \_ REGISTER \_ 回拨) 。

-   打开一个句柄以面向 DirectDraw 表面 (将 **DxApi** 函数标识符设置为 DD \_ DxApi \_ OPENSURFACE) 。

-   取消注册 (**DxApi** 函数标识符设置为 DD \_ DxApi \_ 注销 \_ 回调) 的回调。

-   关闭图柄和内核模式 DirectDraw (**DxApi** 函数标识符设置为 DD \_ DxApi \_ CLOSEHANDLE) 

### <a name="video-port-child-devices-and-power-management"></a>视频端口子设备和电源管理

当使用微型驱动程序时，视频端口子设备（如电视调谐器和显示组合适配器）可以阻止电源状态转换。 当微型驱动程序正在)  (插针或筛选器处于打开状态时，将发生电源状态转换阻塞。 如果已加载微型驱动程序，但未使用任何 pin 或筛选器，电源状态将从 S0 (完全关闭的) 转换为降低电源 (状态，例如 S1、S2、S3 和 S4) 将会出现。 仅当 Stream 类微型驱动程序是视频端口子设备的客户端时，才会阻止电源状态转换。

WHQL 弃权可用于满足此条件的设备，因此供应商仍可获取徽标。

 

