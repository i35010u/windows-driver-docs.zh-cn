---
title: WIA \_ DPC \_ 压缩 \_ 设置
description: WIA \_ DPC \_ COMPRESSION \_ 设置属性包含一个范围或整数列表，用来表示图像质量。
keywords:
- WIA_DPC_COMPRESSION_SETTING 图像设备
topic_type:
- apiref
api_name:
- WIA_DPC_COMPRESSION_SETTING
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3d149c74633b36f4a8864875d4c9c7b31c6937a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793625"
---
# <a name="wia_dpc_compression_setting"></a>WIA \_ DPC \_ 压缩 \_ 设置


WIA \_ DPC \_ COMPRESSION \_ 设置属性包含一个范围或整数列表，用来表示图像质量。

## <span id="ddk_wia_dpc_compression_setting_si"></span><span id="DDK_WIA_DPC_COMPRESSION_SETTING_SI"></span>


属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表或 wia 的 \_ 内容 \_ 范围

访问权限：读/写

<a name="remarks"></a>备注
-------

"WIA \_ DPC \_ 压缩 \_ 设置" 属性旨在大致线性地说明各种场景内容的图像质量。 较小的整数代表较低的质量 (也就是说，最大压缩) ，更大的整数表示较高的质量 (，即最小压缩) 。 设备上的任何可用设置都是相对于该设备的，因此是设备特定的。

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

 

 





