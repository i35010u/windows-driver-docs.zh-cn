---
title: CODECAPI\_音频\_编码器
description: CODECAPI\_音频\_编码器
ms.assetid: c66cbbe1-36dc-4088-8ecd-7663d4503d6e
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71774812c89a4f093f6cf4498a3c55de501b8a36
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543532"
---
# <a name="codecapiaudioencoder"></a>CODECAPI\_音频\_编码器


## <span id="ddk_codecapi_audio_encoder_ks"></span><span id="DDK_CODECAPI_AUDIO_ENCODER_KS"></span>


音频编码器使用的支持 （由用户模式下 KsProperty BASICSUPPORT 查询） 此 GUID 来表示他们对音频编码器。

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
<td><p>Filter</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

（操作数据） 的属性值类型 BOOL 的是，它指定微型驱动程序是否支持音频编码。 值为 **，则返回 TRUE**指示微型驱动程序支持音频编码。 筛选器应支持此 GUID，如果它不是音频编码器。

### <a name="requirements"></a>要求

**标头：** 在中声明*ksmedia.h*。 包括*ksmedia.h*。

### <a name="see-also"></a>另请参阅

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 





