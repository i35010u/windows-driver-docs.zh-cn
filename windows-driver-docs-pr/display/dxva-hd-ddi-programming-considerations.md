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
ms.openlocfilehash: c196caf4797abd694d99c755240c922c1a77f985
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065466"
---
# <a name="dxva-hd-ddi-programming-considerations"></a>DXVA-HD DDI 编程注意事项


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

在用户模式显示驱动程序中实现 [DXVA-HD DDI](dxva-hd-ddi.md) 时，应考虑以下编程技巧：

-   驱动程序必须将 \_ [D3DCAPS9](https://go.microsoft.com/fwlink/p/?linkid=122122)结构**CAPS3**成员中的 D3DCAPS3 DXVAHD (0x00000400L) 位设置为指示它支持 DXVA-hd DDI，否则 Direct3D 运行时将无法调用[**CREATEVIDEOPROCESSOR**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_createvideoprocessor)函数来创建 DXVA-hd 设备。 DirectX 9.0 SDK 文档中介绍了 D3DCAPS9 结构。 驱动程序将 D3DCAPS3 \_ DXVAHD 位设置为响应其[**GetCaps**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)函数的调用，其中 D3DDDICAPS \_ GETD3D9CAPS 值是在 D3DDDIARG 参数指向的[**GetCaps \_ pData**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)结构的**Type**成员中设置的。 *pData*

-   \_ \_ \_ \_ \_ 应用程序级 DXVAHD 表面类型枚举的 DXVAHD 表面类型视频输入私有 \_ 值 \_ 没有相应的 DDI 值。 应用程序为 \_ \_ \_ \_ \_ 以不同格式类型为 CPU 或着色器基础视频处理器插件分配的离屏普通表面设置 DXVAHD 表面类型的视频输入专用值。

-   \_ \_ \_ \_ 应用程序级 DXVAHD 表面类型枚举的 DXVAHD 表面类型视频输出 \_ 值 \_ 对应于[**D3DDDI \_ RESOURCEFLAGS**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_resourceflags)结构的**VideoProcessRenderTarget**位域标志。 当运行时调用驱动程序的[**CREATERESOURCE**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)函数来创建视频处理呈现目标时，Direct3D 运行时将在[**D3DDDIARG \_ CREATERESOURCE**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)结构的**Flags**成员中设置**VideoProcessRenderTarget** 。

-   Direct3D 运行时) 和流状态 (维护两个位块传输。 查询运行时，运行时将返回到应用程序。

-   应用程序级别的 **IDXVAHD \_ VideoProcessor：： GetVideoProcessBltState** 方法没有对应的 DDI 函数。 但是，当应用程序调用 **IDXVAHD \_ VideoProcessor：： GetVideoProcessBltState** 检索视频处理器的专用 bitblt 状态数据时，Direct3D 运行时将调用驱动程序的 [**GetVideoProcessBltStatePrivate**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_getvideoprocessbltstateprivate) 函数。

-   应用程序级别的 **IDXVAHD \_ VideoProcessor：： GetVideoProcessStreamState** 方法没有对应的 DDI 函数。 但是，当应用程序调用 **IDXVAHD \_ VideoProcessor：： GetVideoProcessBltState** 检索视频处理器的专用流状态数据时，Direct3D 运行时将调用该驱动程序的 [**GetVideoProcessStreamStatePrivate**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_getvideoprocessstreamstateprivate) 函数。

-   \_ \_ \_ 应用程序级 DXVAHD 流状态枚举的 DXVAHD 流状态 D3DFORMAT \_ 值 \_ 在[**DXVAHDDDI \_ 流 \_ 状态**](/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_dxvahdddi_stream_state)枚举中没有相应的 DDI 值。 视频处理器插件将 DXVAHD \_ 流 \_ 状态 \_ D3DFORMAT 值用于使用 \_ \_ \_ \_ \_ 应用程序级 DXVAHD \_ surface \_ type 枚举的 DXVAHD 表面类型视频输入私有值分配的图面。

-   DXVAHD \_ 设备 \_ 类型枚举没有对应的 DDI 枚举 (例如，DXVAHDDDI \_ 设备类型不 \_) 。 [**DXVAHDDDI \_ VPDEVCAPS**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_vpdevcaps)结构的第一个成员是保留成员，而应用程序级 DXVAHD VPDEVCAPS 结构的第一个成员 \_ 设置为 \_ \_ **DXVAHD**成员中的 DeviceType 设备类型值。 **DeviceType**成员由运行时或视频处理器插件设置，该插件始终将驱动程序报告为 DXVAHD \_ 设备 \_ 类型的 \_ 硬件。

-   [**DXVAHDDDI \_ 筛选 \_ 范围 \_ 数据**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_filter_range_data)结构的**乘数**成员为浮点值。 驱动程序应使用一个值，该值可精确表示为以2为底的小数部分。 例如，0.25 可以完全表示为以2为底的小数，但0.1 不能。

-   任何 [DXVA 的 DDI](dxva-hd-ddi.md) 函数应返回 S \_ OK、E \_ INVALIDARG 或 E \_ OUTOFMEMORY。

 

