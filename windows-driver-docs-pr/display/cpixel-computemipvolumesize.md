---
title: CPixel ComputeMipVolumeSize 方法
description: CPixel ComputeMipVolumeSize 方法确定将 mipmap 的纹理卷分配所需的内存量。
ms.assetid: f759421a-a41e-4705-8a18-124f7efb059b
keywords:
- ComputeMipVolumeSize 方法显示设备
- ComputeMipVolumeSize 方法显示设备，CPixel 接口
- CPixel 接口显示设备，ComputeMipVolumeSize 方法
topic_type:
- apiref
api_name:
- CPixel.ComputeMipVolumeSize
api_location:
- pixel.hpp
api_type:
- COM
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: c308fcb3462440e902b071e73e608bc7c6ea7370
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555643"
---
# <a name="cpixelcomputemipvolumesize-method"></a>CPixel::ComputeMipVolumeSize 方法


**CPixel::ComputeMipVolumeSize**方法确定将 mipmap 的纹理卷分配所需的内存量。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
static UINT ComputeMipVolumeSize(
   UINT      cpWidth,
   UINT      cpHeight,
   UINT      cpDepth,
   UINT      cLevels,
   D3DFORMAT Format
);
```

<a name="parameters"></a>参数
----------

*cpWidth*以像素为单位的 mipmap 卷指定的宽度。

*cpHeight*以像素为单位的 mipmap 卷指定的高度。

*cpDepth*以像素为单位的 mipmap 卷指定的深度。

*cLevels*指定 mipmap 卷纹理的级别数。

*格式*D3DFORMAT 枚举中的值用于指定的图面上的格式。

<a name="return-value"></a>返回值
------------

返回的大小，以字节为单位的 mipmap 卷。

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

 

 





