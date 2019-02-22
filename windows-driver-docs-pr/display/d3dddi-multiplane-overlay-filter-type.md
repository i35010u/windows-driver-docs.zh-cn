---
title: D3DDDI\_MULTIPLANE\_覆盖\_筛选器\_类型枚举
description: 保留供系统使用。 不要使用它在您的驱动程序中。请注意此结构是仅在使用 Windows Driver Kit (WDK) 8 随附版本与 Windows 8 提供的 D3dumddi.h 标头中可用。 已从更高版本的标头。 .
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
ms.openlocfilehash: 4dbbedd2128f5627539b9ad4f27ab9f896aa3294
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554888"
---
# <a name="d3dddimultiplaneoverlayfiltertype-enumeration"></a>D3DDDI\_MULTIPLANE\_覆盖\_筛选器\_类型枚举


保留供系统使用。 不要使用它在您的驱动程序中。

&gt; \[!请注意\]&gt;此结构是仅在使用 Windows Driver Kit (WDK) 8 随附版本与 Windows 8 提供的 D3dumddi.h 标头中可用。 已从更高版本的标头。

 

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

<span id="D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_BRIGHTNESS"></span><span id="d3dddi_multiplane_overlay_filter_caps_brightness"></span>**D3DDDI\_MULTIPLANE\_覆盖\_筛选器\_CAPS\_亮度**

<span id="D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_CONTRAST"></span><span id="d3dddi_multiplane_overlay_filter_caps_contrast"></span>**D3DDDI\_MULTIPLANE\_覆盖\_筛选器\_CAPS\_对比度**

<span id="D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_HUE"></span><span id="d3dddi_multiplane_overlay_filter_caps_hue"></span>**D3DDDI\_MULTIPLANE\_覆盖\_筛选器\_CAPS\_HUE**

<span id="D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_SATURATION"></span><span id="d3dddi_multiplane_overlay_filter_caps_saturation"></span>**D3DDDI\_MULTIPLANE\_覆盖\_筛选器\_CAPS\_饱和度**

<span id="D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_STRETCH_QUALITY"></span><span id="d3dddi_multiplane_overlay_filter_caps_stretch_quality"></span>**D3DDDI\_MULTIPLANE\_覆盖\_筛选器\_CAPS\_STRETCH\_质量**

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
<td align="left"><p>标头</p></td>
<td align="left">D3dumddi.h</td>
</tr>
</tbody>
</table>

 

 





