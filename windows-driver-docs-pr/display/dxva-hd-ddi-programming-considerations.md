---
title: DXVA-HD DDI 编程注意事项
description: DXVA-HD DDI 编程注意事项
ms.assetid: 84576a8d-67e1-480a-9323-ef34b0900d22
keywords:
- DXVA-HD DDI WDK Windows 7 显示，编程注意事项
- DXVA-HD DDI WDK Server 2008 R2 显示，编程注意事项
- 高清晰视频 WDK Windows 7 显示，DXVA，编程注意事项
- 高清晰视频 WDK Server 2008 R2 显示，DXVA，编程注意事项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f5e809c16a2f71e470a497ea16263b5ee2402f9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839718"
---
# <a name="dxva-hd-ddi-programming-considerations"></a>DXVA-HD DDI 编程注意事项


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

在用户模式显示驱动程序中实现[DXVA-HD DDI](dxva-hd-ddi.md)时，应考虑以下编程技巧：

-   驱动程序必须在[D3DCAPS9](https://go.microsoft.com/fwlink/p/?linkid=122122)结构的**Caps3**成员中设置 D3DCAPS3\_DXVAHD （0x00000400L）位以指明它支持 DXVA-HD DDI，否则 Direct3D 运行时将无法调用[**CreateVideoProcessor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_createvideoprocessor)用于创建 DXVA 设备的函数。 DirectX 9.0 SDK 文档中介绍了 D3DCAPS9 结构。 驱动程序将 D3DCAPS3\_DXVAHD 位设置为响应其[**GetCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)函数的调用，其中 D3DDDICAPS\_GETD3D9CAPS 值是在 [**D3DDDIARG\_GetCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps) *pData*参数指向。

-   DXVAHD\_SURFACE\_类型\_视频\_输入\_应用程序级别的 DXVAHD\_图面\_类型枚举的私有值没有相应的 DDI 值。 应用程序将 DXVAHD\_SURFACE\_类型\_视频\_输入\_以不同格式类型为 CPU 或着色器基础视频处理器插件分配的非屏幕普通表面。

-   DXVAHD\_SURFACE\_类型\_视频\_视频输出值\_类型枚举与 D3DDDI 的**VideoProcessRenderTarget**位域标志相对应[ **\__ RESOURCEFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_resourceflags)结构。 当运行时调用驱动程序的[**CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)函数以创建视频处理时，Direct3D 运行时将在[**D3DDDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)结构的**Flags**成员中设置**VideoProcessRenderTarget**呈现目标。

-   Direct3D 运行时同时保留位块传输（bitblt）和流状态。 查询运行时，运行时将返回到应用程序。

-   应用程序级**IDXVAHD\_VideoProcessor：： GetVideoProcessBltState**方法没有对应的 DDI 函数。 但是，当应用程序调用**IDXVAHD\_VideoProcessor：： GetVideoProcessBltState**检索视频处理器的专用 bitblt 状态数据时，Direct3D 运行时将调用驱动程序的[**GetVideoProcessBltStatePrivate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_getvideoprocessbltstateprivate)才能.

-   应用程序级**IDXVAHD\_VideoProcessor：： GetVideoProcessStreamState**方法没有对应的 DDI 函数。 但是，当应用程序调用**IDXVAHD\_VideoProcessor：： GetVideoProcessBltState**检索视频处理器的专用流状态数据时，Direct3D 运行时将调用该驱动程序的[**GetVideoProcessStreamStatePrivate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_getvideoprocessstreamstateprivate)才能.

-   应用程序级\_DXVAHD 流\_状态枚举的 DXVAHD\_流\_状态\_D3DFORMAT 值在[**DXVAHDDDI\_流\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_dxvahdddi_stream_state)枚举中没有相应的 DDI 值。 视频处理器插件将 DXVAHD\_流\_状态\_D3DFORMAT 值用于使用 DXVAHD\_SURFACE 分配的图面\_类型\_视频\_输入\_应用程序级别的 DXVAHD\_SURFACE\_类型枚举。

-   DXVAHD\_设备\_类型枚举没有对应的 DDI 枚举（例如，DXVAHDDDI\_设备\_类型）。 保留了[**DXVAHDDDI\_VPDEVCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_vpdevcaps)结构的第一个成员，而应用程序级 DXVAHD\_VPDEVCAPS 结构的第一个成员设置为 DXVAHD\_设备\_类型值在**DeviceType**中。职员. **DeviceType**成员由运行时或视频处理器插件设置，它始终将驱动程序报告为 DXVAHD\_设备\_类型\_硬件。

-   [ **\_筛选器\_范围\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_filter_range_data)结构的**乘数**成员是一个浮点值。 驱动程序应使用一个值，该值可精确表示为以2为底的小数部分。 例如，0.25 可以完全表示为以2为底的小数，但0.1 不能。

-   任何[DXVA 的 DDI](dxva-hd-ddi.md)函数应返回\_OK、e\_INVALIDARG 或 e\_OUTOFMEMORY。

 

 





