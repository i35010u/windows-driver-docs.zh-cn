---
title: KSPROPERTY\_DVDCOPY\_DISC\_KEY
description: KSPROPERTY\_DVDCOPY\_光盘\_密钥属性检索 DVD 版权保护身份验证过程的光盘密钥信息。
ms.assetid: 6108040e-b549-4cdc-ae1c-8f453fe5c8c1
keywords:
- KSPROPERTY_DVDCOPY_DISC_KEY 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_DVDCOPY_DISC_KEY
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff053e98431ce088782a8dd01ef9cef0bd8f3cd4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380635"
---
# <a name="kspropertydvdcopydisckey"></a>KSPROPERTY\_DVDCOPY\_DISC\_KEY


KSPROPERTY\_DVDCOPY\_光盘\_密钥属性检索 DVD 版权保护身份验证过程的光盘密钥信息。

## <span id="ddk_ksproperty_dvdcopy_disc_key_ks"></span><span id="DDK_KSPROPERTY_DVDCOPY_DISC_KEY_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567637" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_DISCKEY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567637)"><strong>KS_DVDCOPY_DISCKEY</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KS\_DVDCOPY\_DISCKEY 结构描述的 DVD 光盘密钥。

<a name="remarks"></a>备注
-------

有关光盘密钥的详细信息，请参阅[DVD 版权保护](https://msdn.microsoft.com/library/windows/hardware/ff558736)。

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


[**KS\_DVDCOPY\_DISCKEY**](https://msdn.microsoft.com/library/windows/hardware/ff567637)

 

 






