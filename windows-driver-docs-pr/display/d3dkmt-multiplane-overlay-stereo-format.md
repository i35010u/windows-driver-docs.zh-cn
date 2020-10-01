---
title: D3DKMT \_ MULTIPLANE \_ 叠加 \_ 立体声 \_ 格式枚举
description: 了解 D3DKMT \_ MULTIPLANE \_ 叠加 \_ 立体声 \_ 格式枚举，它保留供系统使用。 请勿在您的驱动程序中使用。
ms.assetid: dd26ac4b-ecef-4b4d-a050-d3e429ff0542
keywords:
- D3DKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT 枚举显示设备
topic_type:
- apiref
api_name:
- D3DKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6a67f18e74faea98569c0e32384e87b85380089c
ms.sourcegitcommit: fc94eb0d5a41ef81c1b3ab91ad725386db0be0c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91603545"
---
# <a name="d3dkmt_multiplane_overlay_stereo_format-enumeration"></a>D3DKMT \_ MULTIPLANE \_ 叠加 \_ 立体声 \_ 格式枚举


预留给系统使用。 请勿在您的驱动程序中使用。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef enum D3DKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT {
  DXGKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT_MONO                = 0,
  D3DKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT_HORIZONTAL          = 1,
  D3DKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT_VERTICAL            = 2,
  DXGKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT_SEPARATE            = 3,
  DXGKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT_MONO_OFFSET         = 4,
  DXGKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT_ROW_INTERLEAVED     = 5,
  DXGKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT_COLUMN_INTERLEAVED  = 6,
  DXGKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT_CHECKERBOARD        = 7
} D3DKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT;
```

<a name="constants"></a>常量
---------

<span id="DXGKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT_MONO"></span><span id="dxgkmt_multiplane_overlay_stereo_format_mono"></span>**DXGKMT \_ MULTIPLANE \_ 叠加 \_ 立体声 \_ 格式 \_ MONO**

<span id="D3DKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT_HORIZONTAL"></span><span id="d3dkmt_multiplane_overlay_stereo_format_horizontal"></span>**D3DKMT \_ MULTIPLANE \_ 叠加 \_ 立体声 \_ 格式（ \_ 水平）**

<span id="D3DKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT_VERTICAL"></span><span id="d3dkmt_multiplane_overlay_stereo_format_vertical"></span>**D3DKMT \_ MULTIPLANE \_ 叠加 \_ 立体声 \_ 格式 \_ 竖**

<span id="DXGKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT_SEPARATE"></span><span id="dxgkmt_multiplane_overlay_stereo_format_separate"></span>**DXGKMT \_ MULTIPLANE \_ 叠加 \_ 立体声 \_ 格式 \_**

<span id="DXGKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT_MONO_OFFSET"></span><span id="dxgkmt_multiplane_overlay_stereo_format_mono_offset"></span>**DXGKMT \_ MULTIPLANE \_ 叠加 \_ 立体声 \_ 格式 \_ MONO \_ 偏移**

<span id="DXGKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT_ROW_INTERLEAVED"></span><span id="dxgkmt_multiplane_overlay_stereo_format_row_interleaved"></span>**DXGKMT \_ MULTIPLANE \_ 叠加 \_ 立体声 \_ 格式 \_ 行 \_ 交错**

<span id="DXGKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT_COLUMN_INTERLEAVED"></span><span id="dxgkmt_multiplane_overlay_stereo_format_column_interleaved"></span>**DXGKMT \_ MULTIPLANE \_ 叠加 \_ 立体声 \_ 格式 \_ 列 \_ 交错**

<span id="DXGKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT_CHECKERBOARD"></span><span id="dxgkmt_multiplane_overlay_stereo_format_checkerboard"></span>**DXGKMT \_ MULTIPLANE \_ 叠加 \_ 立体声 \_ 格式 \_ 棋盘**

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
<td align="left">D3dkmthk</td>
</tr>
</tbody>
</table>

 

 





