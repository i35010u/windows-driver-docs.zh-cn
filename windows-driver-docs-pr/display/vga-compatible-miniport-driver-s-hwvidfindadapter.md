---
title: VGA 兼容的微型端口驱动程序的 HwVidFindAdapter
description: VGA 兼容的微型端口驱动程序的 HwVidFindAdapter
ms.assetid: 4538e95f-e84d-434c-a674-e1d1d4e9e5a0
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，VGA、 HwVidFindAdapter
- VGA WDK 视频微型端口 HwVidFindAdapter
- HwVidFindAdapter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44be0f881df23a4a7805d1e30f236d2bf3175b44
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365083"
---
# <a name="vga-compatible-miniport-drivers-hwvidfindadapter"></a>VGA 兼容的微型端口驱动程序的 HwVidFindAdapter


## <span id="ddk_vga_compatible_miniport_driver_s_hwvidfindadapter_gg"></span><span id="DDK_VGA_COMPATIBLE_MINIPORT_DRIVER_S_HWVIDFINDADAPTER_GG"></span>


兼容的 VGA 的微型端口驱动程序的[ *HwVidFindAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_find_adapter)函数 (或注册表*HwVid...回调*) 必须设置中的以下[**视频\_端口\_CONFIG\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_port_config_info)缓冲区：

-   **NumEmulatorAccessEntries**，指示中的条目数**EmulatorAccessEntries**数组

-   **EmulatorAccessEntries**，指向包含给定的数目的静态数组[**模拟器\_访问\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/miniport/ns-miniport-_emulator_access_entry)-类型元素，每个描述范围的 I/O 端口挂接从 V86 仿真程序，并且默认情况下，转发给*SvgaHwIoPortXxx*函数

    每个条目都包含一个起始 I/O 地址范围长度、 大小的访问是捕获 （UCHAR、 USHORT 或 ULONG） 是否微型端口驱动程序支持的输入或输出字符串数据进行的 I/O 端口，并且微型端口驱动程序提供*SvgaHwIoPortXxx*函数，用于实际验证，并可能，将数据传输。 每个*SvgaHwIoPortXxx*函数中读取的句柄 (**IN**或**REP INSB/INSW/INSD**) 和/或写入 (**出**或**REP OUTSB /OUTSW/OUTSD**) 的 UCHAR、 USHORT 或 ULONG 大小的数据传输。

-   **EmulatorAccessEntriesContext**，指向存储，例如在微型端口驱动程序的设备扩展中，在其中一个区域的微型端口驱动程序*SvgaHwIoPortXxx*函数可以执行批处理的应用程序颁发的序列要求进行验证的说明

-   **VdmPhysicalVideoMemoryAddress**并**VdmPhysicalVideoMemoryLength**，描述一系列必须映射到的视频内存*VDM*地址空间，以支持从 BIOS INT10 调用全屏幕 MS-DOS 应用程序

    微型端口驱动程序可以调用[ **VideoPortInt10** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportint10)时此类应用程序将视频的模式更改为一个微型端口驱动程序的适配器可以支持的功能。

-   **HardwareStateSize**，描述最小存储适配器的硬件状态以响应 IOCTL 所需的字节数\_视频\_保存\_硬件\_状态请求

    当用户切换全屏 MS-DOS 应用程序，在窗口中运行时，微型端口驱动程序必须保存之前显示驱动程序会重新获得控制的视频适配器的适配器状态。 请注意，兼容的 VGA 的微型端口驱动程序还必须支持相互 IOCTL\_视频\_还原\_硬件\_状态请求，因为用户可能会切换到全屏窗口中的应用程序模式。

兼容的 VGA 的微型端口驱动程序的仿真程序访问项指定适配器及其访问范围数组的子集。 仿真程序访问的项可以且通常由映射的访问范围数组中的所有 I/O 端口都设置其[ *HwVidFindAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_find_adapter)函数。 访问范围它对的调用中传递[ **VideoPortSetTrappedEmulatorPorts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportsettrappedemulatorports)、 定义当前 IOPM 并确定由全屏幕 MS-DOS 应用程序，直接访问的 I/O 端口指定的微型端口驱动程序的仿真程序访问项的子集。

 

 





