---
title: CPixel ComputeSurfaceOffset 方法
description: CPixel ComputeSurfaceOffset 方法确定图面的 subrectangular 偏移量。
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
ms.openlocfilehash: e306ce21d0d2cd98aa62dee9bf1dd631a5523284
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834635"
---
# <a name="cpixelcomputesurfaceoffset-method"></a>CPixel：： ComputeSurfaceOffset 方法


**CPixel：： ComputeSurfaceOffset** 方法确定图面的 subrectangular 偏移量。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
static void ComputeSurfaceOffset(
   const D3DSURFACE_DESC *pDescTopLevel,
         BYTE            *pBits,
   const RECT            *pRect,
         D3DLOCKED_RECT  *pLockedRectData
);
```

<a name="parameters"></a>参数
----------

*pDescTopLevel* 指向 \_ 描述图面的 D3DSURFACE DESC 结构的指针。

*pBits* 指向图面的开头的指针; 如果调用方只需要偏移量，则为 **NULL** 。

*pRect* 指向描述 subrectangular 区域的 RECT 结构的指针; 如果调用方只需要图面的开头，则为 **NULL** 。

*pLockedRectData* 指向 D3DLOCKED \_ RECT 结构的指针，该结构接收锁定的矩形区域的指针或偏移量。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

给定表面说明，指向图面的开头，subrectangle， **CPixel：： ComputeSurfaceOffset** 将在 D3DLOCKED 的 pLockedRectData RECT 结构的 **pBits** 成员中返回指针或偏移量 \_ 。 **pLockedRectData**

有关 D3DLOCKED \_ RECT、D3DSURFACE \_ DESC 和 RECT 的详细信息，请参阅 MICROSOFT DirectX SDK 文档。

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
<td align="left">台式机</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Hpp (包含 hpp) </td>
</tr>
</tbody>
</table>

 

 





