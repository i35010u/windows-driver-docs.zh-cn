---
title: CPixel ComputeSurfaceOffset 方法
description: CPixel ComputeSurfaceOffset 方法确定一个面 subrectangular 偏移的量。
ms.assetid: 3589ea80-94f8-418b-895d-c52310536e45
keywords:
- ComputeSurfaceOffset 方法显示设备
- ComputeSurfaceOffset 方法显示设备，CPixel 接口
- CPixel 接口显示设备，ComputeSurfaceOffset 方法
topic_type:
- apiref
api_name:
- CPixel.ComputeSurfaceOffset
api_location:
- pixel.hpp
api_type:
- COM
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: a160240c166a36f15ef9dd7a19206d1e784f2cce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390001"
---
# <a name="cpixelcomputesurfaceoffset-method"></a>CPixel::ComputeSurfaceOffset 方法


**CPixel::ComputeSurfaceOffset**方法确定的一个面 subrectangular 偏移量。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
static void ComputeSurfaceOffset(
   const D3DSURFACE_DESC *pDescTopLevel,
         BYTE            *pBits,
   const RECT            *pRect,
         D3DLOCKED_RECT  *pLockedRectData
);
```

<a name="parameters"></a>Parameters
----------

*pDescTopLevel*指针，指向 D3DSURFACE\_DESC 结构描述图面。

*pBits*面开头的指针或**NULL**如果调用方只需偏移量。

*pRect*描述 subrectangular 区域的 RECT 结构的指针或**NULL**如果调用方只需在图面开头。

*pLockedRectData*指针，指向 D3DLOCKED\_RECT 结构，它接收的指针或对锁定的矩形区域的偏移量。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

给定的图面上的说明的图面上和 subrectangle，开头的指针**CPixel::ComputeSurfaceOffset**返回的指针或偏移量中锁定的矩形区域**pBits**隶属 D3DLOCKED\_RECT 结构的时间**pLockedRectData**。

详细了解 D3DLOCKED\_RECT、 D3DSURFACE\_DESC 和矩形，请参阅 Microsoft DirectX SDK 文档。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left">桌面设备</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Pixel.hpp （包括 Pixel.hpp）</td>
</tr>
</tbody>
</table>

 

 





