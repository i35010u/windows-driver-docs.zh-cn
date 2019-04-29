---
title: D3DKMT\_MULTIPLANE\_覆盖\_属性结构
description: 保留供系统使用。 不要在您的驱动程序中使用。
ms.assetid: 07abf207-62ab-42d1-84b0-74815d1d42b8
keywords:
- D3DKMT_MULTIPLANE_OVERLAY_ATTRIBUTES 结构显示设备
topic_type:
- apiref
api_name:
- D3DKMT_MULTIPLANE_OVERLAY_ATTRIBUTES
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 392b40acbda1732a860c5918685e4b2f016df2ea
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382946"
---
# <a name="d3dkmtmultiplaneoverlayattributes-structure"></a>D3DKMT\_MULTIPLANE\_覆盖\_属性结构


保留供系统使用。 不要在您的驱动程序中使用。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct D3DKMT_MULTIPLANE_OVERLAY_ATTRIBUTES {
  UINT                                         Flags;
  RECT                                         SrcRect;
  RECT                                         DstRect;
#if (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WDDM1_3)
  RECT                                         ClipRect;
#endif
  D3DDDI_ROTATION                              Rotation;
  D3DKMT_MULTIPLANE_OVERLAY_BLEND              Blend;
#if (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WDDM1_3)
  UINT                                         DirtyRectCount;
  RECT                                         pDirtyRects;
#else
  UINT                                         NumFilters;
  void                                         *pFilters;
#endif
  D3DKMT_MULTIPLANE_OVERLAY_VIDEO_FRAME_FORMAT VideoFrameFormat;
  UINT                                         YCbCrFlags;
  D3DKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT      StereoFormat;
  BOOL                                         StereoLeftViewFrame0;
  BOOL                                         StereoBaseViewFrame0;
  DXGKMT_MULTIPLANE_OVERLAY_STEREO_FLIP_MODE   StereoFlipMode;
#if (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WDDM1_3)
  DXGKMT_MULTIPLANE_OVERLAY_STRETCH_QUALITY    StretchQuality;
#endif
} D3DKMT_MULTIPLANE_OVERLAY_ATTRIBUTES;
```

<a name="members"></a>成员
-------

**标志**

**SrcRect**

**DstRect**

**ClipRect**

**旋转**

**blend**

**DirtyRectCount**

**pDirtyRects**

**NumFilters**

**pFilters**

**VideoFrameFormat**

**YCbCrFlags**

**StereoFormat**

**StereoLeftViewFrame0**

**StereoBaseViewFrame0**

**StereoFlipMode**

**StretchQuality**

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

 

 





