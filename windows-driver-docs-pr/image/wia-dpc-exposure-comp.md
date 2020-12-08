---
title: WIA \_ DPC \_ 曝光度 \_ 复合
description: 使用 "WIA \_ DPC \_ 曝光" \_ 复合属性，您可以调整数码相机自动曝光控制的设置点。
keywords:
- WIA_DPC_EXPOSURE_COMP 图像设备
topic_type:
- apiref
api_name:
- WIA_DPC_EXPOSURE_COMP
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c56411d3a232d547a0ec01a6817d59572f98a0a2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840361"
---
# <a name="wia_dpc_exposure_comp"></a>WIA \_ DPC \_ 曝光度 \_ 复合


使用 "WIA \_ DPC \_ 曝光" \_ 复合属性，您可以调整数码相机自动曝光控制的设置点。

## <span id="ddk_wia_dpc_exposure_comp_si"></span><span id="DDK_WIA_DPC_EXPOSURE_COMP_SI"></span>


属性类型： VT \_ I4

有效值： WIA "内容范围" 或 "WIA 内容" \_ \_ \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

你可以使用 "WIA \_ DPC \_ 曝光" \_ 复合属性来调整数码相机自动曝光控制的设置点。 将 WIA \_ DPC \_ 曝露 \_ 复合设置为零不会更改出厂设置的自动曝光级别。

WIA \_ DPC \_ 曝光度复合的单位为 \_ "停止"，缩放比例为1000，以允许使用小数部分的值。 将 WIA \_ DPC \_ 曝露 \_ 复合设置为2000对应于两个 (停止了传感器) 上更多的能量，使图像更亮。 将 WIA \_ DPC \_ 曝露 \_ 复合设置为−1000对应于降低 (传感器) 的一半的风险，使图像变暗。

设置值位于 " (顶点) 单位的" 图像公开曝光 "的" 增量系统 "中。

此属性可表示为一个列表或值范围。 通常，仅当设备将 " [**WIA \_ DPC \_ 曝光 \_ 模式**](wia-dpc-exposure-mode.md) " 属性设置为 "EXPOSUREMODE" 时，才会使用此属性 \_ 。

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

## <a name="see-also"></a>请参阅


[**WIA \_ DPC \_ 曝光 \_ 模式**](wia-dpc-exposure-mode.md)

 

 






