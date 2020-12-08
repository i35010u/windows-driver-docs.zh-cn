---
title: WIA \_ DPC \_ 公开 \_ 索引
description: 使用 "WIA \_ DPC \_ 曝光索引" 属性， \_ 可以模拟数码相机上的电影速度设置。
keywords:
- WIA_DPC_EXPOSURE_INDEX 图像设备
topic_type:
- apiref
api_name:
- WIA_DPC_EXPOSURE_INDEX
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84dd9587b44c5ab1c0fa828f8e68a992d3e063f2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830471"
---
# <a name="wia_dpc_exposure_index"></a>WIA \_ DPC \_ 公开 \_ 索引


使用 "WIA \_ DPC \_ 曝光索引" 属性， \_ 可以模拟数码相机上的电影速度设置。

## <span id="ddk_wia_dpc_exposure_index_si"></span><span id="DDK_WIA_DPC_EXPOSURE_INDEX_SI"></span>


属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表或 wia 的 \_ 内容 \_ 范围

访问权限：读/写

<a name="remarks"></a>备注
-------

电影速度设置对应于 (ASA/) 的 ISO 标识。 通常，设备支持离散枚举值，但可以连续控制一定范围的值。 WIA \_ DPC 曝露索引属性值为 0xffff \_ \_ 对应于自动 ISO 设置。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 Windows Vista 和更高版本的操作系统中已过时，不应再使用。 但是，在 Windows Vista 中仍定义此属性，以与为 Windows Server 2003、Windows XP 和 windows 的早期版本设计的应用程序和设备兼容。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

 





