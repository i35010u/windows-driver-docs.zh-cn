---
title: 纹理格式列表
description: 纹理格式列表
ms.assetid: 5e60d6e3-d0a2-4b52-86cb-06de839f970a
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，纹理格式列表
- 纹理格式列出 WDK DirectX 8。0
- DPIXELFORMAT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c07b45f4f348591ddd1b3ce4af4fc0d53305037
ms.sourcegitcommit: a44ade167cdfb541cf1818e9f9e3726f23f90b66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2020
ms.locfileid: "94361425"
---
# <a name="the-texture-format-list"></a>纹理格式列表


## <span id="ddk_the_texture_format_list_gg"></span><span id="DDK_THE_TEXTURE_FORMAT_LIST_GG"></span>


Direct 8.0 引入了一种用于描述像素格式的新机制。 在以前版本的 DirectDraw 和 Direct3D 像素格式中，数据结构 ( [**DDPIXELFORMAT**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)) ，其中包含有关每个颜色通道的位数以及每个颜色通道的位数 (以及标志和大小字段) 的信息。 DirectX 8.0 中的像素格式是简单的 Dword，用于识别特定像素格式，并与 *fourcc* 兼容 (Direct3D 像素格式只需 fourcc，而不是最小有效字节数为零) 。

DDPIXELFORMAT 数据结构不再通过 API 级接口公开。 但是，它仍在 DDI 级别使用。 驱动程序通过纹理格式数组（其中包含其嵌入式 DDPIXELFORMAT 数据结构的图面说明）来报告其支持的纹理格式。 不过，现在可以使用嵌入的像素格式结构来报告新样式像素格式。 若要使用 DDPIXELFORMAT 数据结构指定新的样式像素格式，请将结构的 **dwFlags** 字段设置为值 DDPF \_ D3DFORMAT，并将新的像素格式标识符存储在 **dwFourCC** 字段中。

此外，某些其他新字段已添加到 DDPIXELFORMAT (新字段已添加为具有现有字段的联合成员，因此数据结构的大小) 相同。 这些字段包括： **dwOperations** 、 **dwPrivateFormatBitCount** 、 **wFlipMSTypes** 和 **wBltMSTypes** 。

DirectX 8.0 DDI 兼容驱动程序应继续通过标准机制（即，全局驱动程序数据结构中所报告的纹理格式列表 ( [**D3DHAL \_ GLOBALDRIVERDATA**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_globaldriverdata)) 和为响应 \_ 来自 [**DdGetDriverInfo**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)的 GUID ZPixelFormats 报告的 Z/模具列表）来报告 DX7 样式表面格式。 但是，驱动程序还应通过下面所述的新的 DirectX 8.0 DDI 机制来报告其所有受支持的表面格式。

DirectX 8.0 DDI 样式表面格式使用 **GetDriverInfo2** 报告。 运行时使用两个 **GetDriverInfo2** 查询类型从驱动程序查询表面格式。 D3DGDI2 \_ 类型 \_ GETFORMATCOUNT 用于请求驱动程序支持的 DirectX 8.0 样式表面格式的数目。 D3DGDI2 \_ 类型 \_ iformatprovider.getformat 用于从驱动程序查询特定的表面格式。

若要处理 D3DGDI2 \_ 类型 \_ GETFORMATCOUNT，驱动程序必须在 [**DD \_ GETFORMATCOUNTDATA**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_getformatcountdata)的 **dwFormatCount** 字段中存储它支持的 DirectX 8.0 DDI 样式表面格式的数目。

当运行时从驱动程序接收到受支持的格式的数目时，它将同时查询每种表面格式，同时还会为 D3DGDI2 类型 Iformatprovider.getformat 类型的 **GetDriverInfo2** 查询 \_ \_ 。 [**Dd \_ GETDRIVERINFODATA**](/windows/win32/api/ddrawint/ns-ddrawint-dd_getdriverinfodata)数据结构的 **lpvData** 字段指向的数据结构为，在本例中为 [**dd \_ GETFORMATDATA**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_getformatdata)。

DirectX 8.0 运行时扫描驱动程序报告的纹理格式列表，检查每个像素格式的 **dwFlags** 字段。 如果任何纹理格式的 **dwFlags** 设置为 DDPF \_ D3DFORMAT，则运行时将此纹理格式列表标识为 DX8 样式，并筛选像素格式未标记为 DDPF D3DFORMAT 的所有纹理格式 \_ 。 此外，DX7 运行时将筛选 DDPF D3DFORMAT 集的任何纹理格式 \_ 。 因此，支持 DX8 DDI 的驱动程序可以返回一个纹理格式列表，其中包含每个受支持格式的两个项，一种是在旧样式中指定，另一个在新样式中。 DX8 运行时使用在新样式中指定的格式，DX7 运行时使用旧样式中指定的格式。

所有受支持的表面格式（如纹理、深度或模具缓冲区或呈现目标）都应通过 **GetDriverInfo2** 机制进行报告。 运行时将忽略通过旧机制返回的纹理和 Z/模具格式 (D3DHAL \_ GLOBALDRIVERDATA 和 GUID \_ ZPixelFormats) 。 不会尝试将这些格式映射到 DirectX 8.0 驱动程序的 DX8 样式格式。 但是，旧版格式将映射到 DirectX 7.0 或更早版本的驱动程序的新样式。 因此，驱动程序必须通过 DirectX 8.0 DDI 报告所有支持的表面格式。 此外，由于旧的运行时不会将新样式图面格式映射到旧样式格式，因此驱动程序将继续使用旧机制来报告 DirectX 7.0 样式图面和 Z/模具格式，这一点非常重要。

