---
title: CPixel ComputeMipVolumeSize 方法
description: CPixel ComputeMipVolumeSize 方法确定分配 mipmap 纹理卷所需的内存量。
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
ms.openlocfilehash: cf6b19f6c7f83210722af2bac8c3c89598ea0746
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834641"
---
# <a name="cpixelcomputemipvolumesize-method"></a>CPixel：： ComputeMipVolumeSize 方法


**CPixel：： ComputeMipVolumeSize** 方法确定分配 mipmap 纹理卷所需的内存量。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
static UINT ComputeMipVolumeSize(
   UINT      cpWidth,
   UINT      cpHeight,
   UINT      cpDepth,
   UINT      cLevels,
   D3DFORMAT Format
);
```

<a name="parameters"></a>参数
----------

*cpWidth* 指定 mipmap 卷的宽度（以像素为单位）。

*cpHeight* 指定 mipmap 卷的高度（以像素为单位）。

*cpDepth* 指定 mipmap 卷的深度（以像素为单位）。

*cLevels* 指定 mipmap 量纹理的级别数。

*格式* 使用 D3DFORMAT 枚举中的值指定表面格式。

<a name="return-value"></a>返回值
------------

返回 mipmap 卷的大小（以字节为单位）。

<a name="remarks"></a>备注
-------

有关 D3DFORMAT 的详细信息，请参阅 Microsoft DirectX SDK 文档。

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

 

 





