---
title: CPixel ComputeSurfaceSize 方法
description: CPixel ComputeSurfaceSize 方法确定分配图面所需的内存量。
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
ms.openlocfilehash: 90b7325c41b3c4506806e8e6fb54b1a47a9c90f1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834623"
---
# <a name="cpixelcomputesurfacesize-method"></a>CPixel：： ComputeSurfaceSize 方法


**CPixel：： ComputeSurfaceSize** 方法确定分配图面所需的内存量。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
static UINT ComputeSurfaceSize(
   UINT      cpWidth,
   UINT      cpHeight,
   D3DFORMAT Format
);
```

<a name="parameters"></a>参数
----------

*cpWidth* 指定图面的宽度（以像素为单位）。

*cpHeight* 指定图面的高度（以像素为单位）。

*格式* 使用 D3DFORMAT 枚举中的值指定表面格式。

<a name="return-value"></a>返回值
------------

返回图面的大小（以字节为单位）。

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

 

 





