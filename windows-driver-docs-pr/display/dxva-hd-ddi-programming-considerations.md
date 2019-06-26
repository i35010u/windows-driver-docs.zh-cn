---
title: DXVA-HD DDI 编程注意事项
description: DXVA-HD DDI 编程注意事项
ms.assetid: 84576a8d-67e1-480a-9323-ef34b0900d22
keywords:
- DXVA HD DDI WDK Windows 7 显示，编程注意事项
- DXVA HD DDI WDK Server 2008 R2 显示，编程注意事项
- 高清晰视频 WDK Windows 7 显示，DXVA HD DDI 编程注意事项
- 高清晰视频 WDK Server 2008 R2 显示，DXVA HD DDI 编程注意事项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12f131d0b9cff25b4da0d64f8446f2475c1f1f58
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384264"
---
# <a name="dxva-hd-ddi-programming-considerations"></a>DXVA-HD DDI 编程注意事项


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

当您实现[DXVA HD DDI](dxva-hd-ddi.md)在用户模式显示驱动程序，应考虑使用以下编程提示：

-   该驱动程序必须设置 D3DCAPS3\_DXVAHD (0x00000400L) 中的位**Caps3**的成员[D3DCAPS9](https://go.microsoft.com/fwlink/p/?linkid=122122)结构，以指示它支持 DXVA HD DDI，否则 Direct3D 运行时将失败若要调用[ **CreateVideoProcessor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_createvideoprocessor)函数来创建 DXVA HD 设备。 D3DCAPS9 结构是 DirectX 9.0 SDK 文档中所述。 驱动程序设置 D3DCAPS3\_DXVAHD 位以响应对的调用其[ **GetCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)函数在其中 D3DDDICAPS\_GETD3D9CAPS 值中设置**类型**的成员[ **D3DDDIARG\_GETCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)结构*pData*参数指向。

-   DXVAHD\_面\_类型\_视频\_输入\_专用值的应用程序级 DXVAHD\_面\_类型枚举具有没有相应的 DDI 值。 应用程序设置 DXVAHD\_面\_类型\_视频\_输入\_一个屏外的普通图面，CPU 或着色器基本视频分配不同的格式类型中的专用值处理器插件。

-   DXVAHD\_面\_类型\_视频\_输出值的应用程序级 DXVAHD\_图面\_类型枚举对应于**VideoProcessRenderTarget**的位域标志[ **D3DDDI\_RESOURCEFLAGS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_resourceflags)结构。 Direct3D 的运行时设置**VideoProcessRenderTarget**中**标志**的成员[ **D3DDDIARG\_CREATERESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)结构，当运行时调用的驱动程序[ **CreateResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)函数来创建视频处理呈现器目标。

-   Direct3D 运行时维护位块传输 (bitblt) 和流状态。 运行时查询时，运行时将返回到应用程序。

-   应用程序级**IDXVAHD\_VideoProcessor::GetVideoProcessBltState**方法有没有相应的 DDI 函数。 但是，当应用程序调用**IDXVAHD\_VideoProcessor::GetVideoProcessBltState**若要检索视频处理器的专用 bitblt 状态数据，Direct3D 运行时将调用驱动程序的[ **GetVideoProcessBltStatePrivate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_getvideoprocessbltstateprivate)函数。

-   应用程序级**IDXVAHD\_VideoProcessor::GetVideoProcessStreamState**方法有没有相应的 DDI 函数。 但是，当应用程序调用**IDXVAHD\_VideoProcessor::GetVideoProcessBltState**若要检索视频处理器的专用流状态数据，Direct3D 运行时将调用驱动程序的[ **GetVideoProcessStreamStatePrivate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_getvideoprocessstreamstateprivate)函数。

-   DXVAHD\_流\_状态\_D3DFORMAT 值的应用程序级 DXVAHD\_流\_状态枚举已没有对应的 DDI 值[ **DXVAHDDDI\_流\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-_dxvahdddi_stream_state)枚举。 视频处理器插件使用 DXVAHD\_流\_状态\_D3DFORMAT 值使用 DXVAHD 分配面的\_图面\_类型\_视频\_输入\_专用值的应用程序级 DXVAHD\_图面\_类型枚举。

-   DXVAHD\_设备\_类型枚举具有没有相应的 DDI 枚举 (例如，没有 DXVAHDDDI\_设备\_类型)。 第一个成员[ **DXVAHDDDI\_VPDEVCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvahdddi_vpdevcaps)而保留结构的第一个成员的应用程序级 DXVAHD\_VPDEVCAPS 结构设置为 DXVAHD\_设备\_中的类型值**DeviceType**成员。 **DeviceType**成员设置由运行时或插件，视频的处理器将始终报告驱动程序，因为 DXVAHD\_设备\_类型\_硬件。

-   **乘数**的成员[ **DXVAHDDDI\_筛选器\_范围\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvahdddi_filter_range_data)结构是浮点值。 该驱动程序应使用一个值，可以完全为基的 2 个分数表示。 例如，可以完全为基的 2 个分数表示 0.25，但不能 0.1。

-   任何[DXVA HD DDI](dxva-hd-ddi.md)函数应返回 S\_确定，E\_INVALIDARG 或 E\_发生内存不足。

 

 





