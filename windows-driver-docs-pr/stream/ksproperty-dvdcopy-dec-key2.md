---
title: KSPROPERTY\_DVDCOPY\_DEC\_KEY2
description: KSPROPERTY\_DVDCOPY\_DEC\_KEY2 属性检索的第二个总线密钥更高版本提供给解码器 DVD 版权保护身份验证过程的一部分。
ms.assetid: 48e62fec-773d-46b6-838b-5e1e457cb6a3
keywords:
- KSPROPERTY_DVDCOPY_DEC_KEY2 流式处理媒体设备
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
ms.openlocfilehash: 42262ae408d995d3bc25626f7c8795bc899a5474
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373059"
---
# <a name="kspropertydvdcopydeckey2"></a>KSPROPERTY\_DVDCOPY\_DEC\_KEY2


KSPROPERTY\_DVDCOPY\_DEC\_KEY2 属性检索的第二个总线密钥更高版本提供给解码器 DVD 版权保护身份验证过程的一部分。

## <span id="ddk_ksproperty_dvdcopy_dec_key2_ks"></span><span id="DDK_KSPROPERTY_DVDCOPY_DEC_KEY2_KS"></span>


### <a name="usage-summary-table"></a>使用率摘要表

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
<th>Get</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ks_dvdcopy_buskey" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_BUSKEY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ks_dvdcopy_buskey)"><strong>KS_DVDCOPY_BUSKEY</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KS\_DVDCOPY\_BUSKEY 结构描述 DVD 解码器的第二个总线键。

<a name="remarks"></a>备注
-------

第二个总线密钥的详细信息，请参阅[DVD 版权保护](https://docs.microsoft.com/windows-hardware/drivers/stream/dvd-copyright-protection)。

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
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KS\_DVDCOPY\_BUSKEY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ks_dvdcopy_buskey)

 

 






