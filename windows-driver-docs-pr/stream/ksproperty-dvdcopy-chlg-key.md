---
title: KSPROPERTY\_DVDCOPY\_CHLG\_KEY
description: KSPROPERTY\_DVDCOPY\_CHLG\_键属性将传输的 DVD 解码器和 DVD 驱动器提供的总线质询密钥。
ms.assetid: 744ea965-29dc-401f-8f68-7d63b58b6151
keywords:
- KSPROPERTY_DVDCOPY_CHLG_KEY 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_DVDCOPY_CHLG_KEY
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37c409bc89a4bda598119b083e659601e4623c61
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534456"
---
# <a name="kspropertydvdcopychlgkey"></a>KSPROPERTY\_DVDCOPY\_CHLG\_KEY


KSPROPERTY\_DVDCOPY\_CHLG\_键属性将传输的 DVD 解码器和 DVD 驱动器提供的总线质询密钥。

## <span id="ddk_ksproperty_dvdcopy_chlg_key_ks"></span><span id="DDK_KSPROPERTY_DVDCOPY_CHLG_KEY_KS"></span>


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
<td><p>是</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567636" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_CHLGKEY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567636)"><strong>KS_DVDCOPY_CHLGKEY</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KS\_DVDCOPY\_CHLGKEY 结构描述的总线质询密钥。

<a name="remarks"></a>备注
-------

有关**获取**请求时，DVD 解码器提供其总线质询键。 有关**设置**请求时，DVD 解码器提供从 DVD 驱动器的总线质询密钥。

有关总线质询密钥的详细信息，请参阅[DVD 版权保护](https://msdn.microsoft.com/library/windows/hardware/ff558736)。

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
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KS\_DVDCOPY\_CHLGKEY**](https://msdn.microsoft.com/library/windows/hardware/ff567636)

 

 






