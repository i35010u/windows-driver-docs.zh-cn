---
title: KSPROPERTY\_DVDCOPY\_标题\_键
description: KSPROPERTY\_DVDCOPY\_TITLE\_键属性将从 DVD 版权保护身份验证过程的当前内容检索标题键信息。
ms.assetid: 7c07bf75-cbc4-4319-a1a6-4f05d228d91a
keywords:
- KSPROPERTY_DVDCOPY_TITLE_KEY 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_DVDCOPY_TITLE_KEY
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6784166e9a9747d35695f87e428b88b7a1a05a0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827121"
---
# <a name="ksproperty_dvdcopy_title_key"></a>KSPROPERTY\_DVDCOPY\_标题\_键


KSPROPERTY\_DVDCOPY\_TITLE\_键属性将从 DVD 版权保护身份验证过程的当前内容检索标题键信息。

## <span id="ddk_ksproperty_dvdcopy_title_key_ks"></span><span id="DDK_KSPROPERTY_DVDCOPY_TITLE_KEY_KS"></span>


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
<td><p>无</p></td>
<td><p>“是”</p></td>
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_titlekey" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_TITLEKEY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_titlekey)"><strong>KS_DVDCOPY_TITLEKEY</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是说明当前标题键的 DVDCOPY\_TITLEKEY 结构的 KS\_。

<a name="remarks"></a>备注
-------

有关标题键的详细信息，请参阅[DVD 版权保护](https://docs.microsoft.com/windows-hardware/drivers/stream/dvd-copyright-protection)。

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


[**KS\_DVDCOPY\_TITLEKEY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_titlekey)

 

 






