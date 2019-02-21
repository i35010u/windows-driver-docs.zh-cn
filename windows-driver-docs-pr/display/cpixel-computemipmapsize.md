---
title: CPixel ComputeMipMapSize 方法
description: CPixel ComputeMipMapSize 方法确定需分配 mipmap 的纹理的内存量。
ms.assetid: f60883df-9200-4ae7-b130-21a6892e14be
keywords:
- ComputeMipMapSize 方法显示设备
- ComputeMipMapSize 方法显示设备，CPixel 接口
- CPixel 接口显示设备，ComputeMipMapSize 方法
topic_type:
- apiref
api_name:
- CPixel.ComputeMipMapSize
api_location:
- pixel.hpp
api_type:
- COM
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1b0b53d200d35fe0291f6c0b1d4f0471dc67ec46
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526717"
---
# <a name="cpixelcomputemipmapsize-method"></a>CPixel::ComputeMipMapSize 方法


**CPixel::ComputeMipMapSize**方法确定需分配 mipmap 的纹理的内存量。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
static UINT  ComputeMipMapSize(
   UINT      cpWidth,
   UINT      cpHeight,
   UINT      cLevels,
   D3DFORMAT Format
);
```

<a name="parameters"></a>参数
----------

*cpWidth*指定以像素为单位的 mipmap 的纹理的宽度。

*cpHeight*指定以像素为单位的 mipmap 的纹理的高度。

*cLevels*指定 mipmap 的纹理的级别数。

*格式*D3DFORMAT 枚举中的值用于指定的图面上的格式。

<a name="return-value"></a>返回值
------------

返回的大小，以字节为单位的 mipmap 的纹理。

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
<td align="left"><p>标头</p></td>
<td align="left">Pixel.hpp （包括 Pixel.hpp）</td>
</tr>
</tbody>
</table>

 

 





