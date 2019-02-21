---
title: CPixel ComputeMipMapOffset 方法
description: CPixel ComputeMipMapOffset 方法确定 mipmap 的纹理的子级偏移量。
ms.assetid: f7181577-c94f-436c-8b3e-2befe89185d3
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
ms.openlocfilehash: 86a978b34682f7a263f07c6d782f4ef8862376f5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519872"
---
# <a name="cpixelcomputemipmapoffset-method"></a>CPixel::ComputeMipMapOffset 方法


**CPixel::ComputeMipMapOffset**方法确定 mipmap 的纹理的子级偏移量。

<a name="syntax"></a>语法
------

```cpp
static void  ComputeMipMapOffset(
   const D3DSURFACE_DESC *pDescTopLevel,
         UINT            iLevel,
         BYTE            *pBits,
   const RECT            *pRect,
         D3DLOCKED_RECT  *pLockedRectData
);
```

<a name="parameters"></a>参数
----------

*pDescTopLevel*指针，指向 D3DSURFACE\_DESC 结构描述 mipmap 的纹理的最高级别。

*iLevel*指定确定偏移量的 mipmap 的纹理的级别。

*pBits* mipmap 的纹理的顶级开头的指针或**NULL**如果调用方只需偏移量。

*pRect*描述 subrectangular 区域的 RECT 结构的指针或**NULL**如果调用方只需子项的开头。

*pLockedRectData*指针，指向 D3DLOCKED\_RECT 结构，它接收的指针或对锁定的矩形区域的偏移量。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

最高级别和 subrectangle，在给定的图面上的说明、 mipmap 的纹理的级别和指针**CPixel::ComputeMipMapOffset**返回的指针或偏移量中锁定的矩形区域**pBits**隶属 D3DLOCKED\_RECT 结构**pLockedRectData**。

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
<td align="left"><p>标头</p></td>
<td align="left">Pixel.hpp （包括 Pixel.hpp）</td>
</tr>
</tbody>
</table>

 

 





