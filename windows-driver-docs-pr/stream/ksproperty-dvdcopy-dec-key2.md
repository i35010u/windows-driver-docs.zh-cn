---
title: KSPROPERTY \_ DVDCOPY \_ DEC \_ KEY2
description: KSPROPERTY \_ DVDCOPY \_ DEC \_ KEY2 属性检索作为 DVD 版权保护身份验证过程的一部分提供给解码器的第二个总线密钥。
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
ms.openlocfilehash: ee4360028a4bf3a327365e40fb8b03eeb6f14e10
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106706"
---
# <a name="ksproperty_dvdcopy_dec_key2"></a>KSPROPERTY \_ DVDCOPY \_ DEC \_ KEY2


KSPROPERTY \_ DVDCOPY \_ DEC \_ KEY2 属性检索作为 DVD 版权保护身份验证过程的一部分提供给解码器的第二个总线密钥。

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
<th>获取</th>
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
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_buskey" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_BUSKEY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_buskey)"><strong>KS_DVDCOPY_BUSKEY</strong></a></p></td>
</tr>
</tbody>
</table>

 

) 操作数据 (的属性值是用于 \_ \_ 描述 DVD 解码器的第二个总线密钥的 KS DVDCOPY BUSKEY 结构。

<a name="remarks"></a>备注
-------

有关第二个总线密钥的详细信息，请参阅 [DVD 版权保护](./dvd-copyright-protection.md)。

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
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KS \_ DVDCOPY \_ BUSKEY**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_buskey)

