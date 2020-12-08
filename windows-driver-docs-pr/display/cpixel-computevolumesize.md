---
title: CPixel ComputeVolumeSize 方法
description: CPixel ComputeVolumeSize 方法决定了分配卷所需的内存量。
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
ms.openlocfilehash: 3d4ee5fb473243f8ae79653e5c4dd633b53a0512
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834621"
---
# <a name="cpixelcomputevolumesize-method"></a>CPixel：： ComputeVolumeSize 方法


**CPixel：： ComputeVolumeSize** 方法确定分配卷所需的内存量。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
static UINT ComputeVolumeSize(
   UINT      cpWidth,
   UINT      cpHeight,
   UINT      cpDepth,
   D3DFORMAT Format
);
```

<a name="parameters"></a>参数
----------

*cpWidth* 指定卷的宽度（以像素为单位）。

*cpHeight* 指定卷的高度（以像素为单位）。

*cpDepth* 指定卷的深度（以像素为单位）。

*格式* 使用 D3DFORMAT 枚举中的值指定表面格式。

<a name="return-value"></a>返回值
------------

返回卷的大小（以字节为单位）。

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

 

 





