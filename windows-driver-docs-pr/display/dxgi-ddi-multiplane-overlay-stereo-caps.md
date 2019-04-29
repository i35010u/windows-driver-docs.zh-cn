---
title: DXGI\_DDI\_MULTIPLANE\_覆盖\_立体声\_CAPS 枚举
description: 保留供系统使用。 不要使用它在您的驱动程序中。
ms.assetid: 28017595-06d5-48ff-91d7-0e084d1e92de
keywords:
- DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS 枚举显示设备
topic_type:
- apiref
api_name:
- DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS
api_location:
- Dxgiddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: a69ab7c28e10e17e98e8f75699ee1e9f58aa2c43
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387239"
---
# <a name="dxgiddimultiplaneoverlaystereocaps-enumeration"></a>DXGI\_DDI\_MULTIPLANE\_覆盖\_立体声\_CAPS 枚举


保留供系统使用。 不要使用它在您的驱动程序中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef enum DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS {
  DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS_SEPARATE            = 0x1,
  DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS_ROW_INTERLEAVED     = 0x4,
  DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS_COLUMN_INTERLEAVED  = 0x8,
  DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS_CHECKERBOARD        = 0x10,
  DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS_FLIP_MODE           = 0x20
} DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS;
```

<a name="constants"></a>常量
---------

<span id="DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS_SEPARATE"></span><span id="dxgi_ddi_multiplane_overlay_stereo_caps_separate"></span>**DXGI\_DDI\_MULTIPLANE\_覆盖\_立体声\_CAPS\_单独**

<span id="DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS_ROW_INTERLEAVED"></span><span id="dxgi_ddi_multiplane_overlay_stereo_caps_row_interleaved"></span>**DXGI\_DDI\_MULTIPLANE\_覆盖\_立体声\_CAPS\_行\_交叉存取**

<span id="DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS_COLUMN_INTERLEAVED"></span><span id="dxgi_ddi_multiplane_overlay_stereo_caps_column_interleaved"></span>**DXGI\_DDI\_MULTIPLANE\_覆盖\_立体声\_CAPS\_列\_交叉存取**

<span id="DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS_CHECKERBOARD"></span><span id="dxgi_ddi_multiplane_overlay_stereo_caps_checkerboard"></span>**DXGI\_DDI\_MULTIPLANE\_覆盖\_立体声\_CAPS\_棋盘**

<span id="DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS_FLIP_MODE"></span><span id="dxgi_ddi_multiplane_overlay_stereo_caps_flip_mode"></span>**DXGI\_DDI\_MULTIPLANE\_覆盖\_立体声\_CAPS\_翻转\_模式**

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
<td align="left">Dxgiddi.h</td>
</tr>
</tbody>
</table>

 

 





