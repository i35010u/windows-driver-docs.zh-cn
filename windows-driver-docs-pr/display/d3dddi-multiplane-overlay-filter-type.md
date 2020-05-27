---
title: D3DDDI \_ MULTIPLANE \_ 覆盖 \_ 筛选器 \_ 类型枚举
description: 预留给系统使用。 不要在您的驱动程序中使用它。请注意，此结构仅在随 Windows 8 随附的 Windows 驱动程序工具包（WDK）版本8随附的 D3dumddi 标头中可用。 它已从标头的更高版本中删除。.
ms.assetid: ceca0ed8-7d46-45e1-86cb-3d0506d26328
keywords:
- D3DDDI_MULTIPLANE_OVERLAY_FILTER_TYPE 枚举显示设备
topic_type:
- apiref
api_name:
- D3DDDI_MULTIPLANE_OVERLAY_FILTER_TYPE
api_location:
- D3dumddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 718cfd5e6e6f0cfe54e50aebbc94a21758240877
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83852130"
---
# <a name="d3dddi_multiplane_overlay_filter_type-enumeration"></a>D3DDDI \_ MULTIPLANE \_ 覆盖 \_ 筛选器 \_ 类型枚举


预留给系统使用。 不要在您的驱动程序中使用它。

> [!NOTE]
> 此结构仅在随 Windows 8 随附的 Windows 驱动程序工具包（WDK）版本8随附的 D3dumddi 标头中可用。 它已从标头的更高版本中删除。

 

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef enum _D3DDDI_MULTIPLANE_OVERLAY_FILTER_TYPE {
  D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_BRIGHTNESS       = 0x1,
  D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_CONTRAST         = 0x2,
  D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_HUE              = 0x4,
  D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_SATURATION       = 0x8,
  D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_STRETCH_QUALITY  = 0x10
} D3DDDI_MULTIPLANE_OVERLAY_FILTER_TYPE;
```

<a name="constants"></a>常量
---------

<span id="D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_BRIGHTNESS"></span><span id="d3dddi_multiplane_overlay_filter_caps_brightness"></span>**D3DDDI \_ MULTIPLANE \_ 叠加 \_ 滤镜 \_ 帽 \_ 亮度**

<span id="D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_CONTRAST"></span><span id="d3dddi_multiplane_overlay_filter_caps_contrast"></span>**D3DDDI \_ MULTIPLANE \_ 叠加 \_ 滤镜 \_ 端 \_ 对比度**

<span id="D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_HUE"></span><span id="d3dddi_multiplane_overlay_filter_caps_hue"></span>**D3DDDI \_ MULTIPLANE \_ 叠加 \_ 筛选器 \_ 大写 \_ 色调**

<span id="D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_SATURATION"></span><span id="d3dddi_multiplane_overlay_filter_caps_saturation"></span>**D3DDDI \_ MULTIPLANE \_ 叠加 \_ 滤镜 \_ 帽 \_ 饱和度**

<span id="D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_STRETCH_QUALITY"></span><span id="d3dddi_multiplane_overlay_filter_caps_stretch_quality"></span>**D3DDDI \_ MULTIPLANE \_ 叠加 \_ 筛选器 \_ 大写 \_ 拉伸 \_ 质量**

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>最低受支持的客户端</p></td>
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">D3dumddi</td>
</tr>
</tbody>
</table>

 

 





