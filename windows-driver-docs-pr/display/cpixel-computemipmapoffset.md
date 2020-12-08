---
title: CPixel ComputeMipMapOffset 方法
description: CPixel ComputeMipMapOffset 方法确定 mipmap 纹理的子偏移量。
keywords:
- ComputeMipMapOffset 方法显示设备
- ComputeMipMapOffset 方法显示设备，CPixel 接口
- CPixel 接口显示设备，ComputeMipMapOffset 方法
topic_type:
- apiref
api_name:
- CPixel.ComputeMipMapOffset
api_location:
- pixel.hpp
api_type:
- COM
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 03785805b250ce697a3c33a45631c650ada20987
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839113"
---
# <a name="cpixelcomputemipmapoffset-method"></a>CPixel：： ComputeMipMapOffset 方法


**CPixel：： ComputeMipMapOffset** 方法确定 mipmap 纹理的子偏移量。

<a name="syntax"></a>语法
------

```cpp
static void  ComputeMipMapOffset(
   const D3DSURFACE_DESC *pDescTopLevel,
         UINT            iLevel,
         BYTE            *pBits,
   const RECT            *pRect,
         D3DLOCKED_RECT  *pLockedRectData
);
```

<a name="parameters"></a>参数
----------

*pDescTopLevel* 指向 \_ 描述 mipmap 纹理顶层的 D3DSURFACE DESC 结构的指针。

*iLevel* 指定确定偏移量的 mipmap 纹理的级别。

*pBits* 指向 mipmap 纹理顶级的开头的指针; 如果调用方只需要偏移量，则为 **NULL** 。

*pRect* 指向描述 subrectangular 区域的 RECT 结构的指针; 如果调用方只需要子层的开头，则为 **NULL** 。

*pLockedRectData* 指向 D3DLOCKED \_ RECT 结构的指针，该结构接收锁定的矩形区域的指针或偏移量。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

给定的图面说明、mipmap 纹理的指针、指向顶层的指针和 subrectangle、 **CPixel：： ComputeMipMapOffset** 会将指针或偏移量返回到 pBits 的 **D3DLOCKED 成员 pLockedRectData 成员的成员** \_ 。 **pLockedRectData**

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

 

 





