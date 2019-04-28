---
title: WIA\_IPA\_RAW\_BITS\_每\_通道
description: WIA\_IPA\_RAW\_BITS\_每\_通道属性包含的每个颜色通道中的位数。
ms.assetid: 541d5409-b095-4bf0-bdc7-cc56d416ed43
keywords:
- WIA_IPA_RAW_BITS_PER_CHANNEL 成像设备
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
ms.openlocfilehash: e56a74db4ed907929088e64602f3d8de5f04e146
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346843"
---
# <a name="wiaiparawbitsperchannel"></a>WIA\_IPA\_RAW\_BITS\_每\_通道


WIA\_IPA\_RAW\_BITS\_每\_通道属性包含的每个颜色通道中的位数。

## <span id="ddk_wia_ipa_raw_bits_per_channel_si"></span><span id="DDK_WIA_IPA_RAW_BITS_PER_CHANNEL_SI"></span>


属性类型：VT\_UI1 | VT\_VECTOR

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

WIA\_IPA\_RAW\_BITS\_每\_应报告的信道属性，为包含有任意数量的字节值的矢量通道，其中的第一个字节对应于中的位数第一个通道，第二个字节设置为第二个通道和等的比特数。 向量必须包含为任意数量的条目[ **WIA\_IPA\_通道\_每\_像素**](wia-ipa-channels-per-pixel.md)属性报告有通道。 驱动程序设置 WIA\_IPA\_每个通道\_像素时应用程序设置[ **WIA\_IPA\_格式**](wia-ipa-format.md)到 WiaImgFmt\_原始。

WIA\_IPA\_RAW\_BITS\_每\_通道是类似于[ **WIA\_IPA\_位\_每\_通道**](wia-ipa-bits-per-channel.md)属性 （它用于以外 RAW 格式）。

下表描述所需的数目的 WIA 中的条目\_IPA\_RAW\_BITS\_每\_通道定义 WIA\_IPA\_数据类型值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>WIA_IPA_DATATYPE 值</th>
<th>所需的 WIA_IPA_RAW_BITS_PER_CHANNEL 中的条目数</th>
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
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA\_IPA\_CHANNELS\_PER\_PIXEL**](wia-ipa-channels-per-pixel.md)

[**WIA\_IPA\_DATATYPE**](wia-ipa-datatype.md)

[**WIA\_IPA\_格式**](wia-ipa-format.md)

 

 






