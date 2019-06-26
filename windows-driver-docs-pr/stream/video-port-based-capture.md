---
title: 基于视频端口的捕获
description: 基于视频端口的捕获
ms.assetid: 84cc1ee3-142c-4dae-9f5c-0dde66cc3df9
keywords:
- 配置 WDK 视频捕获的筛选器图形、 视频基于端口的捕获
- 视频基于端口的捕获 WDK 视频捕获
- 视频端口 pin WDK 视频捕获
- VPEs WDK 视频捕获
- 视频端口扩展 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 839f5f95264526de19bdf4e593d417a066af3dea
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385375"
---
# <a name="video-port-based-capture"></a>基于视频端口的捕获


基于视频的端口的捕获设备必须提供连接到的视频端口管理器的视频端口 pin。 视频端口 pin 允许基于硬件的传输，以显示而无需 CPU 或外围组件互连 (PCI) 总线开销预览流。 单独 pin 提供捕获功能 (例如，当捕获的视频必须写入到磁盘)。 在捕获过程中，捕获缓冲区提供给显示驱动程序，它由总线主控填充缓冲区。 捕获微型驱动程序和显示驱动程序之间的交互都进行了更多详细信息稍后在本部分中并在[内核模式视频传输](https://docs.microsoft.com/windows-hardware/drivers/display/kernel-mode-video-transport)。

在系统上运行 Microsoft Windows 98 SE 或 Windows 2000，覆盖 Mixer 筛选器 （更高版本操作系统中的视频端口管理器筛选器的一部分） 不支持的视频端口连接辅助监视器上。 在这种情况下将 pin 连接失败。 运行 Windows Millennium Edition (Windows Me) 和 Windows XP 的系统上支持的视频端口连接辅助监视器上。

如果设备支持 VBI 捕获，它通常会公开两个其他的 pin:VPVBI 和 VBI。 视频端口管理器筛选器使用 VPVBI pin 来分配 VBI 捕获的视频端口图面。 VBI pin 本身提供了原始 VBI 示例。

下图显示了 VPVBI 和 VBI 捕获不同的路径。

![说明了 vpvbi 和 vbi 捕获不同的路径的关系图](images/video-port-capture.gif)

特定于此类型的筛选器关系图的属性集都会[KSPROPSETID\_VPConfig 和 KSPROPSETID\_VPVBIConfig](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-vpconfig-and-kspropsetid-vpvbiconfig)并[PROPSETID\_分配器\_控制](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-allocator-control)。

### <a name="using-the-video-port-extensions-vpes"></a>使用视频端口扩展 (VPEs)

**注意：** 以下各段仅适用于前面的下一版本的 Windows Vista 的操作系统。 如果显示驱动程序将使用新 Windows Vista 驱动程序显示模型 (LDDM)，将在 Windows Vista 中禁用 VPE。

可以使用视频捕获微型驱动程序[ **DxApi** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxapi/nf-dxapi-dxapi)函数与流式处理视频通过视频端口总线捕获之间传输的捕获的微型端口驱动程序进行通信硬件和显示硬件。 流的 NTSC、 PAL 或 SECAM 视频，顺序字段组成，并且只能包含遮蔽 (VBI) 和时间码 （同步水平和垂直同步） 数据。 视频流特征，包括维度，颜色格式，频率、 缩放和裁剪配置在用户模式下通过 VPE DirectDraw 接口。 流式处理已开始后， **DxApi**然后调用在内核模式下捕获单个帧。 若要支持显示更改，例如更改分辨率或切换进出全屏命令提示，微型驱动程序微型端口驱动程序还必须进行注册，以便能够响应此类显示的视频捕获，请更改事件。

VPEs 并**DxApi**到 DirectDraw DDI 使用 DirectX 5.0 引入了函数。 **DxApi**受 Windows 2000 和更高版本操作系统中的微型端口驱动程序。 虚拟显示微型端口驱动程序 (miniVDD) 支持**DxApi**在 Windows 98 和 Windows Me 操作系统上。 启用内核模式视频传输使用**DxApi**，WDM 视频捕获微型驱动程序必须包括*ddkmapi.h* (DirectDraw 内核模式 API) 标头文件和具有链接*dxapi.lib*库。 **DxApi**库使用导出的功能*dxapi.sys*。 *DxApi.sys*可仅 DirectDraw 加载时由于**DxApi**是到 DirectDraw DDI VPEs 的一部分。

**DxApi**是一个单一的内核模式 API，通过公开*DxApi.sys*。 视频端口扩展是一种用户模式 API 所公开*DDraw.dll*。 视频捕获微型驱动程序必须进行多个不同调用到**DxApi**来设置和配置用于正确地流式传输的视频端口硬件。

**DxApi**是封装多个函数标识符的单个函数。 微型驱动程序的第一个参数中传递所需的函数标识符**DxApi**。 对其余的参数**DxApi**适用于为结构对应于函数标识符和长度的缓冲区的微型驱动程序分配的缓冲区。 函数的大小和格式的输入和输出缓冲区的行为取决于指定的函数标识符。 中记录了此行为[DxApi 函数以及标识符](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

WDK 提供了两个示例驱动程序，用于演示如何实现**DxApi**功能。 ATIWDM 示例需要特定硬件存在才可运行。 TestCap 示例不需要的硬件和在所有平台。 GraphEdt 工具可用于与任一示例进行交互。

视频捕获微型驱动程序必须调用的常用函数**DxApi**执行如下：

-   打开的句柄内核模式 DirectDraw (**DxApi**函数标识符设置为 DD\_DXAPI\_OPENDIRECTDRAW)。 必须执行此操作在 IRQL = 被动\_级别。

-   获取硬件视频端口的内核模式功能 (**DxApi**函数标识符设置为 DD\_DXAPI\_GETKERNELCAPS)。

-   注册回调来处理 DirectDraw 事件，如模式切换到全屏显示命令提示符 (**DxApi**函数标识符设置为 DD\_DXAPI\_注册\_回调)。

-   打开的句柄目标 DirectDraw 表面 (**DxApi**函数标识符设置为 DD\_DXAPI\_OPENSURFACE)。

-   取消注册回调 (**DxApi**函数标识符设置为 DD\_DXAPI\_注销\_回调)。

-   关闭句柄以及关于内核模式 DirectDraw 表面 (**DxApi**函数标识符设置为 DD\_DXAPI\_CLOSEHANDLE)

### <a name="video-port-child-devices-and-power-management"></a>视频端口子设备和电源管理

视频端口子设备，例如 TV 调谐器和显示组合适配器时微型驱动程序正在使用阻止电源状态转换。 当微型驱动程序正在使用阻止电源状态转换时发生 （pin 或筛选器已打开）。 如果微型驱动程序加载，但在使用具有没有 pin 或筛选器，将发生从 S0 （完全支持） 的电源状态转换为较低的电源状态 （例如，S1、 S2、 S3 和 S4）。 Stream 类微型驱动程序是客户端的视频端口子设备的电源状态转换阻止仅出现。

WHQL 豁免是可用于满足此条件，以便供应商仍可以获取徽标的设备。

 

 




