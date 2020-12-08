---
title: WIA \_ IPA \_ \_ \_ 每通道原始 \_ 位数
description: WIA \_ IPA \_ RAW \_ BITS \_ PER \_ 通道属性包含每个颜色通道中的位数。
keywords:
- WIA_IPA_RAW_BITS_PER_CHANNEL 图像设备
topic_type:
- apiref
api_name:
- WIA_IPA_RAW_BITS_PER_CHANNEL
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5783f2013070c4661e29cb80ad98d53a4bf1dc4e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817237"
---
# <a name="wia_ipa_raw_bits_per_channel"></a>WIA \_ IPA \_ \_ \_ 每通道原始 \_ 位数


WIA \_ IPA \_ RAW \_ BITS \_ PER \_ 通道属性包含每个颜色通道中的位数。

## <span id="ddk_wia_ipa_raw_bits_per_channel_si"></span><span id="DDK_WIA_IPA_RAW_BITS_PER_CHANNEL_SI"></span>


属性类型： VT \_ UI1 |VT \_ 矢量

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

\_应将 "WIA IPA \_ RAW \_ 位 \_ / \_ 通道" 属性报告为包含与通道数量相同的字节值的向量，其中第一个字节对应于第一个通道中的位数，第二个字节对应于第二个通道中的位数，依此类推。 矢量必须包含多个条目，因为 [**\_ \_ \_ 每个 \_ 像素的 WIA IPA 通道**](wia-ipa-channels-per-pixel.md) 属性报告都有通道。 \_ \_ \_ 当应用程序将 [**wia \_ IPA \_ 格式**](wia-ipa-format.md)设置为 WiaImgFmt RAW 时，驱动程序将为每个像素设置 wia IPA 通道 \_ 。

WIA \_ IPA \_ \_ \_ 每个 \_ 通道的原始位与 [**wia \_ IPA \_ \_ 每 \_ 通道的位数**](wia-ipa-bits-per-channel.md) 不同 (，它用于原始) 以外的格式。

下表描述了 \_ \_ \_ \_ \_ 对于定义的 wia \_ IPA \_ 数据类型值，每个通道的 WIA IPA 原始位中所需的项数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>WIA_IPA_DATATYPE 值</th>
<th>WIA_IPA_RAW_BITS_PER_CHANNEL 中所需的条目数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_DATA_DITHER</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>WIA_DATA_GRAYSCALE</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DATA_RAW_BGR</p></td>
<td><p>3</p></td>
</tr>
<tr class="even">
<td><p>WIA_DATA_RAW_CMY</p></td>
<td><p>3</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DATA_RAW_CMYK</p></td>
<td><p>4</p></td>
</tr>
<tr class="even">
<td><p>WIA_DATA_RAW_RGB</p></td>
<td><p>3</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DATA_RAW_YUV</p></td>
<td><p>3</p></td>
</tr>
<tr class="even">
<td><p>WIA_DATA_RAW_YUVK</p></td>
<td><p>4</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DATA_THRESHOLD</p></td>
<td><p>1</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA \_ IPA \_ \_ 每像素通道数 \_**](wia-ipa-channels-per-pixel.md)

[**WIA \_ IPA \_ 数据类型**](wia-ipa-datatype.md)

[**WIA \_ IPA \_ 格式**](wia-ipa-format.md)

 

 






