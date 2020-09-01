---
title: KSPROPERTY \_ DVDCOPY \_ CHLG \_ KEY
description: KSPROPERTY \_ DVDCOPY \_ CHLG \_ KEY 属性用于传输 DVD 解码器和 dvd 驱动器提供的总线质询密钥。
ms.assetid: 744ea965-29dc-401f-8f68-7d63b58b6151
keywords:
- KSPROPERTY_DVDCOPY_CHLG_KEY 流媒体设备
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
ms.openlocfilehash: b3cdafbac8d9f2bc4a8549a9481806f71451d6ae
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186557"
---
# <a name="ksproperty_dvdcopy_chlg_key"></a>KSPROPERTY \_ DVDCOPY \_ CHLG \_ KEY


KSPROPERTY \_ DVDCOPY \_ CHLG \_ KEY 属性用于传输 DVD 解码器和 dvd 驱动器提供的总线质询密钥。

## <span id="ddk_ksproperty_dvdcopy_chlg_key_ks"></span><span id="DDK_KSPROPERTY_DVDCOPY_CHLG_KEY_KS"></span>


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
<td><p>是</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_chlgkey" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_CHLGKEY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_chlgkey)"><strong>KS_DVDCOPY_CHLGKEY</strong></a></p></td>
</tr>
</tbody>
</table>

 

) 操作数据 (的属性值是 \_ \_ 用于描述总线质询密钥的 KS DVDCOPY CHLGKEY 结构。

<a name="remarks"></a>备注
-------

对于 **Get** 请求，DVD 解码器会提供其总线质询密钥。 对于 **设置** 请求，dvd 解码器是 dvd 驱动器中的总线质询密钥提供的。

有关总线质询密钥的详细信息，请参阅 [DVD 版权保护](./dvd-copyright-protection.md)。

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


[**KS \_ DVDCOPY \_ CHLGKEY**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_chlgkey)

 

