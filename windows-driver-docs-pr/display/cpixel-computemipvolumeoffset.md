---
title: CPixel ComputeMipVolumeOffset 方法
description: CPixel ComputeMipVolumeOffset 方法确定 mipmap 卷纹理的子宗卷偏移量。
ms.assetid: 4fb2f49a-2c1a-4b07-bbd3-76c4e345b243
keywords:
- ComputeMipVolumeOffset 方法显示设备
- ComputeMipVolumeOffset 方法显示设备，CPixel 接口
- CPixel 接口显示设备，ComputeMipVolumeOffset 方法
topic_type:
- apiref
api_name:
- CPixel.ComputeMipVolumeOffset
api_location:
- pixel.hpp
api_type:
- COM
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: f05d5372ef430cc729bfe3a4d4fea6cac0108750
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548316"
---
# <a name="cpixelcomputemipvolumeoffset-method"></a>CPixel::ComputeMipVolumeOffset 方法


**CPixel::ComputeMipVolumeOffset**方法确定 mipmap 卷纹理的子宗卷偏移量。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
static void  ComputeMipVolumeOffset(
   const D3DVOLUME_DESC *pDescTopLevel,
         UINT           iLevel,
         BYTE           *pBits,
   const D3DBOX         *pBox,
   const D3DLOCKED_BOX  *pLockedBoxData
);
```

<a name="parameters"></a>参数
----------

*pDescTopLevel*指针，指向 D3DVOLUME\_DESC 结构描述 mipmap 的纹理卷的最高级别。

*iLevel*指定确定偏移量的 mipmap 卷级别。

*pBits* mipmap 卷纹理的顶级开头的指针或**NULL**如果调用方只需偏移量。

*pBox*描述子宗卷的 D3DBOX 结构的指针或**NULL**如果调用方只需子项的开头。

*pLockedBoxData*指针，指向 D3DLOCKED\_框结构，它接收的指针或锁定的卷区域偏移量。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

最高级别和子宗卷，在给定的图面上的说明、 mipmap 卷的级别和指针**CPixel::ComputeMipVolumeOffset**返回的指针或偏移量到锁定的框区域**pBits**隶属 D3DLOCKED\_框中结构的时间**pLockedBoxData**。

详细了解 D3DLOCKED\_中，D3DVOLUME\_DESC，以及 D3DBOX，请参阅 Microsoft DirectX SDK 文档。

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

 

 





