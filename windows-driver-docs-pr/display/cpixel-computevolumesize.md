---
title: CPixel ComputeVolumeSize 方法
description: CPixel ComputeVolumeSize 方法确定要将卷分配所需的内存量。
ms.assetid: 85e00793-8c30-41a4-91b0-9f0503a6ce09
keywords:
- ComputeVolumeSize 方法显示设备
- ComputeVolumeSize 方法显示设备，CPixel 接口
- CPixel 接口显示设备，ComputeVolumeSize 方法
topic_type:
- apiref
api_name:
- CPixel.ComputeVolumeSize
api_location:
- pixel.hpp
api_type:
- COM
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: e217c5fa904d17115a7fcc52181b9dfccacf66c0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389995"
---
# <a name="cpixelcomputevolumesize-method"></a>CPixel::ComputeVolumeSize 方法


**CPixel::ComputeVolumeSize**方法确定要将卷分配所需的内存量。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
static UINT ComputeVolumeSize(
   UINT      cpWidth,
   UINT      cpHeight,
   UINT      cpDepth,
   D3DFORMAT Format
);
```

<a name="parameters"></a>Parameters
----------

*cpWidth*指定的宽度以像素为单位的数据量。

*cpHeight*指定以像素为单位的数据量的高度。

*cpDepth*指定以像素为单位的数据量的深度。

*格式*D3DFORMAT 枚举中的值用于指定的图面上的格式。

<a name="return-value"></a>返回值
------------

返回的大小，以字节为单位的数据量。

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

 

 





