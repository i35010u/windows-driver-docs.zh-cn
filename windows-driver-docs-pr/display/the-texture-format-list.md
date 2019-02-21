---
title: 纹理格式列表
description: 纹理格式列表
ms.assetid: 5e60d6e3-d0a2-4b52-86cb-06de839f970a
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示纹理格式的属性列
- 纹理格式列出了 WDK DirectX 8.0
- DPIXELFORMAT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea327bef458a156b3b663da7041de9890c896ce9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541275"
---
# <a name="the-texture-format-list"></a>纹理格式列表


## <span id="ddk_the_texture_format_list_gg"></span><span id="DDK_THE_TEXTURE_FORMAT_LIST_GG"></span>


直接 8.0 引入了新的机制，用于描述像素格式。 在以前版本的 DirectDraw 和 Direct3D 像素格式所述的一种数据结构 (**DDPIXELFORMAT** （Direct3D 像素格式是只需使用所有 Fourcc 但为零的最低有效字节）。

通过 API 级别接口不再公开 DDPIXELFORMAT 数据结构。 但是，它仍在使用 DDI 级别。 该驱动程序报告通过纹理格式数组组成的图面上的其嵌入 DDPIXELFORMAT 数据结构说明其支持的纹理格式。 但是，这些嵌入的像素格式结构，现在可以使用报告新样式像素格式。 若要指定使用 DDPIXELFORMAT 数据结构的新样式像素格式，请设置**dwFlags**字段的结构与值 DDPF\_D3DFORMAT 和存储新的像素格式中的标识符**dwFourCC**字段。

此外，新的某些其他字段具有已添加到 DDPIXELFORMAT （新字段添加为具有现有字段的联合的成员因此数据结构的大小相同）。 这些字段包括： **dwOperations**， **dwPrivateFormatBitCount**，并**wFlipMSTypes**并**wBltMSTypes**。

DirectX 8.0 DDI 符合驱动程序应通过标准机制，继续报告 DX7 样式图面上格式，即纹理格式列表中报告全局驱动程序数据结构 ([**D3DHAL\_GLOBALDRIVERDATA**](https://msdn.microsoft.com/library/windows/hardware/ff545963)) 和 Z/模具列表在为 GUID 的响应中报告\_从 ZPixelFormats [ **DdGetDriverInfo**](https://msdn.microsoft.com/library/windows/hardware/ff549404)。 但是，该驱动程序还应该报告所有其支持的图面上格式通过新的 DirectX 8.0 DDI 机制，如下所述。

使用报告 DirectX 8.0 DDI 样式图面上格式**GetDriverInfo2**。 两个**GetDriverInfo2**查询类型由运行时查询图面上的格式从驱动程序。 D3DGDI2\_类型\_GETFORMATCOUNT 用于请求的驱动程序支持 DirectX 8.0 样式图面上格式数。 D3DGDI2\_类型\_GETFORMAT 使用来自驱动程序特定的图面格式的查询。

若要处理 D3DGDI2\_类型\_GETFORMATCOUNT，驱动程序必须存储数量的 DirectX 8.0 DDI 样式图面上的格式，它支持**dwFormatCount**字段[ **DD\_GETFORMATCOUNTDATA**](https://msdn.microsoft.com/library/windows/hardware/ff551566)。

当运行时已收到来自驱动程序支持的格式的数时，它然后查询图面上的每个格式反过来使用**GetDriverInfo2**查询类型 D3DGDI2\_类型\_GETFORMAT。 指向数据结构**lpvData**字段[ **DD\_GETDRIVERINFODATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551550)数据结构后，在这种情况下， [ **DD\_GETFORMATDATA**](https://msdn.microsoft.com/library/windows/hardware/ff551569)。

DirectX 8.0 运行时就会扫描纹理格式列表报告的驱动程序检查**dwFlags**字段的每个像素格式。 如果有任何纹理格式**dwFlags**设置为 DDPF\_D3DFORMAT，然后在运行时标识为 DX8 样式此纹理格式列表和筛选所有纹理格式的像素格式不标记为 DDPF\_D3DFORMAT。 此外，DX7 运行时筛选器具有 DDPF 任何纹理格式\_D3DFORMAT 设置。 因此，支持 DX8 DDI 的驱动程序可以返回包含两个条目的每个受支持的格式，一个指定旧样式中，一个在新的纹理格式列表。 DX8 运行时使用的新样式中指定的格式和 DX7 运行时使用的旧样式中指定的格式。

所有支持的图面上的格式，如纹理、 深度或模具缓冲区或呈现器目标，则应通过报告**GetDriverInfo2**机制。 在运行时将忽略的纹理和 Z/模具格式返回通过旧机制 (D3DHAL\_GLOBALDRIVERDATA 和 GUID\_ZPixelFormats)。 不会尝试将这些格式映射到 DX8 样式格式的 DirectX 8.0 驱动程序。 但是，旧格式映射到新样式 DirectX 7.0 或更早的驱动程序。 因此，驱动程序必须报告所有受支持的图面上通过 DirectX 8.0 DDI 的格式。 此外，由于旧的运行时不会映射到旧样式格式图面上的新样式格式很重要的驱动程序会继续以通过旧的机制报告 DirectX 7.0 样式面和 Z/模具格式。

 

 





