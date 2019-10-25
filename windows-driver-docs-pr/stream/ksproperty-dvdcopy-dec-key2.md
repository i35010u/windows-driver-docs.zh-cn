---
title: KSPROPERTY\_DVDCOPY\_DEC\_KEY2
description: KSPROPERTY\_DVDCOPY\_DEC\_KEY2 属性检索第二个总线密钥，该总线密钥稍后作为 DVD 版权保护过程的一部分提供给解码器。
ms.assetid: 48e62fec-773d-46b6-838b-5e1e457cb6a3
keywords:
- KSPROPERTY_DVDCOPY_DEC_KEY2 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_DVDCOPY_DEC_KEY2
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc936e9eebd09379302362dcbdd407b6e8b0bc75
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843328"
---
# <a name="ksproperty_dvdcopy_dec_key2"></a>KSPROPERTY\_DVDCOPY\_DEC\_KEY2


KSPROPERTY\_DVDCOPY\_DEC\_KEY2 属性检索第二个总线密钥，该总线密钥稍后作为 DVD 版权保护过程的一部分提供给解码器。

## <span id="ddk_ksproperty_dvdcopy_dec_key2_ks"></span><span id="DDK_KSPROPERTY_DVDCOPY_DEC_KEY2_KS"></span>


### <a name="usage-summary-table"></a>使用情况摘要表

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>“获取”</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>“是”</p></td>
<td><p>无</p></td>
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_buskey" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_BUSKEY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_buskey)"><strong>KS_DVDCOPY_BUSKEY</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一个 KS\_DVDCOPY\_BUSKEY 结构，描述 DVD 解码器的第二个总线密钥。

<a name="remarks"></a>备注
-------

有关第二个总线密钥的详细信息，请参阅[DVD 版权保护](https://docs.microsoft.com/windows-hardware/drivers/stream/dvd-copyright-protection)。

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
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KS\_DVDCOPY\_BUSKEY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_buskey)

 

 






