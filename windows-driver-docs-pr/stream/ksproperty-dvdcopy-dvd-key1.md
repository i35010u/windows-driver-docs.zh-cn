---
title: KSPROPERTY\_DVDCOPY\_DVD\_KEY1
description: KSPROPERTY\_DVDCOPY\_DVD\_KEY1 属性检索的第一个总线键向提供的更高版本解码器 DVD 版权保护身份验证过程的一部分。
ms.assetid: df4fd5a0-d890-4695-b8ec-951dd0e4e1d5
keywords:
- KSPROPERTY_DVDCOPY_DVD_KEY1 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_DVDCOPY_DVD_KEY1
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3dae27734f18e5c0f3ea04c9e64e0753c650d64
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380631"
---
# <a name="kspropertydvdcopydvdkey1"></a>KSPROPERTY\_DVDCOPY\_DVD\_KEY1


KSPROPERTY\_DVDCOPY\_DVD\_KEY1 属性检索的第一个总线键向提供的更高版本解码器 DVD 版权保护身份验证过程的一部分。

## <span id="ddk_ksproperty_dvdcopy_dvd_key1_ks"></span><span id="DDK_KSPROPERTY_DVDCOPY_DVD_KEY1_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567635" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_BUSKEY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567635)"><strong>KS_DVDCOPY_BUSKEY</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KS\_DVDCOPY\_BUSKEY 结构描述的 DVD 解码器第一个总线键。

<a name="remarks"></a>备注
-------

第一个总线密钥的详细信息，请参阅[DVD 版权保护](https://msdn.microsoft.com/library/windows/hardware/ff558736)。

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


[**KS\_DVDCOPY\_BUSKEY**](https://msdn.microsoft.com/library/windows/hardware/ff567635)

 

 






