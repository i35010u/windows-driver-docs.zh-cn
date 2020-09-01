---
title: 将 Windows NT 4.0 微型端口驱动程序转换为 Windows 2000 版本
description: 将 Windows NT 4.0 微型端口驱动程序转换为 Windows 2000 版本
ms.assetid: a55192c6-3de4-4433-8825-3393f2bce04a
keywords:
- 视频微型端口驱动程序 WDK Windows 2000、多个 Windows 版本、转换 Windows NT 4.0 驱动程序
- 转换视频微型端口驱动程序 WDK Windows 2000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e807b9f46c74965475449a1e652365c9ffded84
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065674"
---
# <a name="converting-a-windows-nt-40-miniport-driver-to-windows-2000"></a>将 Windows NT 4.0 微型端口驱动程序转换为 Windows 2000 版本


## <span id="ddk_converting_a_windows_nt_4_0_miniport_driver_to_windows_2000_gg"></span><span id="DDK_CONVERTING_A_WINDOWS_NT_4_0_MINIPORT_DRIVER_TO_WINDOWS_2000_GG"></span>


良好的 Windows NT 4.0 和以前的微型端口驱动程序可以轻松成为 Windows 2000 和更高版本的微型端口驱动程序。 下面是在 Windows 2000 和更高版本的微型端口驱动程序中提供即插即用支持所需的一些更新：

-   请参阅 [ (Windows 2000) 型号的视频微型端口驱动程序中的即插即用和电源管理 ](plug-and-play-and-power-management-in-video-miniport-drivers--windows-.md) ，以获取必须实现的新函数的列表。 请确保将 [**视频 \_ HW \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data) 的新成员初始化为指向这些新函数。

-   在[**DriverEntry**](./driverentry-of-video-miniport-driver.md)函数中更新对[**VideoPortInitialize**](/windows-hardware/drivers/ddi/video/nf-video-videoportinitialize)的调用。 第四个参数 (*HwContext*) 在 Windows 2000 和更高版本上必须为 **NULL** 。

-   更新 [*HwVidFindAdapter*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter) 函数。 对于可枚举总线上的设备，必须更改 *HwVidFindAdapter* ，如下所示：

    -   删除大部分设备检测代码。 这是因为对 Windows 2000 上的 [*HwVidFindAdapter*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter) 的调用意味着 PnP 管理器已检测到该设备。
    -   调用 [**VideoPortGetAccessRanges**](/windows-hardware/drivers/ddi/video/nf-video-videoportgetaccessranges) 以获取设备将响应的与总线相关的物理地址。 PnP 管理器会分配这些地址。
    -   如果驱动程序支持多种设备类型，则确定设备的类型。
    -   忽略 [*再次*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter) 参数。 这是因为，系统只会对每个设备调用 *HwVidFindAdapter* 一次。

    对于 nonenumerable 总线（如 ISA）上的设备，PnP 仍会尝试启动该设备，但 [*HwVidFindAdapter*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter) 负责确定设备是否确实存在。

-   更新 **。** 驱动程序的 INF 文件的制造节，以包括设备和供应商 ID。 这是必需的，以便 PnP 管理器可以将设备与其 INF 文件相关联。 Windows NT 4.0 和更新的 Windows 2000 及更高版本的示例 **。制造** 部分如下所示：

    ```cpp
    [ABC.Mfg]   ; Windows NT V4.0 INF
    %ABC% ABC Graphics Accelerator A = abc
    %ABC% ABC Graphics Accelerator B = abc

    [ABC.Mfg]   ; Windows 2000 and later INF
    %ABC% ABC Graphics Accelerator A = abc, PCI\VEN_ABCD&DEV_0123
    %ABC% ABC Graphics Accelerator B = abc, PCI\VEN_ABCD&DEV_4567
    ```

您可以使用驱动程序开发工具包随附的 *geninf.exe* 工具 (的 DDK) 生成 INF。  (在 Windows 驱动程序工具包中的 DDK 之前 \[ \] ) 。但是请记住， *geninf.exe* 不会为 WINDOWS NT 4.0 创建 INF。 如果你打算支持 Windows NT 4.0，则必须修改 *geninf.exe* 生成的 INF 文件。 有关更多详细信息，请参阅 [创建图形 INF 文件](creating-graphics-inf-files.md) 。

Windows 2000 和更高版本视频端口支持作为旧驱动程序的 Windows NT 4.0 小型端口驱动程序。 当系统正在运行时，不能从系统中删除旧微型端口驱动程序的图形适配器，也不能在添加到正在运行的系统时，自动检测到旧版微型端口驱动程序。

 

