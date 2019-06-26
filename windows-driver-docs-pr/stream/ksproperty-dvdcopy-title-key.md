---
title: KSPROPERTY\_DVDCOPY\_TITLE\_KEY
description: KSPROPERTY\_DVDCOPY\_标题\_键属性从 DVD 版权保护身份验证过程的当前内容中检索的标题项信息。
ms.assetid: 7c07bf75-cbc4-4319-a1a6-4f05d228d91a
keywords:
- KSPROPERTY_DVDCOPY_TITLE_KEY 流式处理媒体设备
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
ms.openlocfilehash: 241366e9e12a42f83248a94db912d124aa5b4f93
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368114"
---
# <a name="kspropertydvdcopytitlekey"></a>KSPROPERTY\_DVDCOPY\_TITLE\_KEY


KSPROPERTY\_DVDCOPY\_标题\_键属性从 DVD 版权保护身份验证过程的当前内容中检索的标题项信息。

## <span id="ddk_ksproperty_dvdcopy_title_key_ks"></span><span id="DDK_KSPROPERTY_DVDCOPY_TITLE_KEY_KS"></span>


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
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ks_dvdcopy_titlekey" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_TITLEKEY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ks_dvdcopy_titlekey)"><strong>KS_DVDCOPY_TITLEKEY</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KS\_DVDCOPY\_TITLEKEY 结构，描述当前标题项。

<a name="remarks"></a>备注
-------

有关标题项的详细信息，请参阅[DVD 版权保护](https://docs.microsoft.com/windows-hardware/drivers/stream/dvd-copyright-protection)。

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


[**KS\_DVDCOPY\_TITLEKEY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ks_dvdcopy_titlekey)

 

 






