---
title: CODECAPI\_音频\_编码器
description: CODECAPI\_音频\_编码器
ms.assetid: c66cbbe1-36dc-4088-8ecd-7663d4503d6e
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef9f7774d0c85f8c0296993a9b6dfbe6d08520fa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844730"
---
# <a name="codecapi_audio_encoder"></a>CODECAPI\_音频\_编码器


## <span id="ddk_codecapi_audio_encoder_ks"></span><span id="DDK_CODECAPI_AUDIO_ENCODER_KS"></span>


音频编码器使用此 GUID 的支持（由用户模式 KsProperty BASICSUPPORT 查询）来指示它们是音频编码器。

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
<td><p>Filter</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>型</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）的类型为 BOOL，并指定微型驱动程序是否支持音频编码。 如果值为**TRUE** ，则表示微型驱动程序支持音频编码。 如果不是音频编码器，则筛选器不应支持此 GUID。

### <a name="requirements"></a>要求

**标头：** 在*ksmedia*中声明。 包括*ksmedia*。

### <a name="see-also"></a>另请参阅

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

 





