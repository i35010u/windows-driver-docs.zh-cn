---
title: CPixel ComputeMipVolumeOffset 方法
description: CPixel ComputeMipVolumeOffset 方法确定 mipmap 量纹理的 subvolume 偏移量。
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
ms.openlocfilehash: e48cdead7d3a6debb8e19b3a3d9476a718547a2f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834643"
---
# <a name="cpixelcomputemipvolumeoffset-method"></a>CPixel：： ComputeMipVolumeOffset 方法


**CPixel：： ComputeMipVolumeOffset** 方法确定 mipmap 量纹理的 subvolume 偏移量。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
static void  ComputeMipVolumeOffset(
   const D3DVOLUME_DESC *pDescTopLevel,
         UINT           iLevel,
         BYTE           *pBits,
   const D3DBOX         *pBox,
   const D3DLOCKED_BOX  *pLockedBoxData
);
```

<a name="parameters"></a>参数
----------

*pDescTopLevel* 指向 \_ 描述 mipmap 纹理量顶层的 D3DVOLUME DESC 结构的指针。

*iLevel* 指定确定偏移量的 mipmap 卷的级别。

*pBits* 指向 mipmap 卷纹理顶层的开头的指针; 如果调用方只需要偏移量，则为 **NULL** 。

*pBox* 指向 D3DBOX 结构的指针，该结构描述 subvolume; 如果调用方只需要子部分的开头，则为 **NULL** 。

*pLockedBoxData* 指向 D3DLOCKED \_ 框结构的指针，该结构接收锁定卷区域的指针或偏移量。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

给定了表面说明，mipmap 卷的级别、指向顶层的指针和 subvolume、 **CPixel：： ComputeMipVolumeOffset** 将在 pBits 的 **D3DLOCKED 成员的 pLockedBoxData 成员** 中返回指针或偏移量 \_ 。 **pLockedBoxData**

有关 D3DLOCKED \_ BOX、D3DVOLUME \_ DESC 和 D3DBOX 的详细信息，请参阅 MICROSOFT DirectX SDK 文档。

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

 

 





