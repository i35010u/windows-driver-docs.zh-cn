---
title: D3DKMT\_MULTIPLANE\_覆盖\_立体声\_格式枚举
description: 保留供系统使用。 不要在您的驱动程序中使用。
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
ms.openlocfilehash: 69b8bf854f4365b10048906c84efb2f34b0260f4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382662"
---
# <a name="d3dkmtmultiplaneoverlaystereoformat-enumeration"></a>D3DKMT\_MULTIPLANE\_覆盖\_立体声\_格式枚举


保留供系统使用。 不要在您的驱动程序中使用。

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

<span id="DXGKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT_MONO"></span><span id="dxgkmt_multiplane_overlay_stereo_format_mono"></span>**DXGKMT\_MULTIPLANE\_覆盖\_立体声\_格式\_MONO**

<span id="D3DKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT_HORIZONTAL"></span><span id="d3dkmt_multiplane_overlay_stereo_format_horizontal"></span>**D3DKMT\_MULTIPLANE\_覆盖\_立体声\_格式\_水平**

<span id="D3DKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT_VERTICAL"></span><span id="d3dkmt_multiplane_overlay_stereo_format_vertical"></span>**D3DKMT\_MULTIPLANE\_覆盖\_立体声\_格式\_垂直**

<span id="DXGKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT_SEPARATE"></span><span id="dxgkmt_multiplane_overlay_stereo_format_separate"></span>**DXGKMT\_MULTIPLANE\_覆盖\_立体声\_格式\_单独**

<span id="DXGKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT_MONO_OFFSET"></span><span id="dxgkmt_multiplane_overlay_stereo_format_mono_offset"></span>**DXGKMT\_MULTIPLANE\_覆盖\_立体声\_格式\_MONO\_偏移量**

<span id="DXGKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT_ROW_INTERLEAVED"></span><span id="dxgkmt_multiplane_overlay_stereo_format_row_interleaved"></span>**DXGKMT\_MULTIPLANE\_覆盖\_立体声\_格式\_行\_交叉存取**

<span id="DXGKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT_COLUMN_INTERLEAVED"></span><span id="dxgkmt_multiplane_overlay_stereo_format_column_interleaved"></span>**DXGKMT\_MULTIPLANE\_覆盖\_立体声\_格式\_列\_交叉存取**

<span id="DXGKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT_CHECKERBOARD"></span><span id="dxgkmt_multiplane_overlay_stereo_format_checkerboard"></span>**DXGKMT\_MULTIPLANE\_覆盖\_立体声\_格式\_棋盘**

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
<td align="left">D3dkmthk.h</td>
</tr>
</tbody>
</table>

 

 





