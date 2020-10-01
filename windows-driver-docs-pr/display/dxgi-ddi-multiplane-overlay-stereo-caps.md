---
title: DXGI \_ DDI \_ MULTIPLANE \_ 叠加 \_ 立体声 \_ cap 枚举
description: 了解 DXGI \_ DDI \_ MULTIPLANE \_ 叠加 \_ 立体声 \_ cap 枚举，它保留供系统使用。 不要在您的驱动程序中使用它。
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
ms.openlocfilehash: 481f6174840f868e4e7e1705ad40fa16603ce029
ms.sourcegitcommit: fc94eb0d5a41ef81c1b3ab91ad725386db0be0c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91603673"
---
# <a name="dxgi_ddi_multiplane_overlay_stereo_caps-enumeration"></a>DXGI \_ DDI \_ MULTIPLANE \_ 叠加 \_ 立体声 \_ cap 枚举


预留给系统使用。 不要在您的驱动程序中使用它。

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

<span id="DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS_SEPARATE"></span><span id="dxgi_ddi_multiplane_overlay_stereo_caps_separate"></span>**DXGI \_ DDI \_ MULTIPLANE \_ 叠加 \_ 立体声 \_ CAP \_**

<span id="DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS_ROW_INTERLEAVED"></span><span id="dxgi_ddi_multiplane_overlay_stereo_caps_row_interleaved"></span>**DXGI \_ DDI \_ MULTIPLANE \_ 覆盖 \_ 立体声 \_ CAP \_ 行 \_ 交错**

<span id="DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS_COLUMN_INTERLEAVED"></span><span id="dxgi_ddi_multiplane_overlay_stereo_caps_column_interleaved"></span>**DXGI \_ DDI \_ MULTIPLANE \_ 叠加 \_ 立体声 \_ 大写字母 \_ 列 \_ 交错**

<span id="DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS_CHECKERBOARD"></span><span id="dxgi_ddi_multiplane_overlay_stereo_caps_checkerboard"></span>**DXGI \_ DDI \_ MULTIPLANE \_ 叠加 \_ 立体声 \_ 大写字母 \_**

<span id="DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS_FLIP_MODE"></span><span id="dxgi_ddi_multiplane_overlay_stereo_caps_flip_mode"></span>**DXGI \_ DDI \_ MULTIPLANE \_ 叠加 \_ 立体声 \_ CAP \_ 翻转 \_ 模式**

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
<td align="left">Dxgiddi</td>
</tr>
</tbody>
</table>

 

 





