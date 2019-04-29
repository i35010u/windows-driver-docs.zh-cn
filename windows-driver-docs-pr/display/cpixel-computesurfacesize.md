---
title: CPixel ComputeSurfaceSize 方法
description: CPixel ComputeSurfaceSize 方法确定要分配一个面所需的内存量。
ms.assetid: aeee0757-b381-4579-abae-1190399f3a0d
keywords:
- ComputeSurfaceSize 方法显示设备
- ComputeSurfaceSize 方法显示设备，CPixel 接口
- CPixel 接口显示设备，ComputeSurfaceSize 方法
topic_type:
- apiref
api_name:
- CPixel.ComputeSurfaceSize
api_location:
- pixel.hpp
api_type:
- COM
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 38a0f1072efb3d4a664c053e6e1ddd61af5fce71
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389998"
---
# <a name="cpixelcomputesurfacesize-method"></a>CPixel::ComputeSurfaceSize 方法


**CPixel::ComputeSurfaceSize**方法确定要分配一个面所需的内存量。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
static UINT ComputeSurfaceSize(
   UINT      cpWidth,
   UINT      cpHeight,
   D3DFORMAT Format
);
```

<a name="parameters"></a>Parameters
----------

*cpWidth*指定的宽度以像素为单位的图面。

*cpHeight*以像素为单位的图面中指定的高度。

*格式*D3DFORMAT 枚举中的值用于指定的图面上的格式。

<a name="return-value"></a>返回值
------------

返回的大小，以字节为单位在图面。

<a name="remarks"></a>备注
-------

有关 D3DFORMAT 详细信息，请参阅 Microsoft DirectX SDK 文档。

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

 

 





