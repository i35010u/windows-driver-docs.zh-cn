---
title: KSPROPERTY\_DVDCOPY\_SET\_COPY\_STATE
description: KSPROPERTY\_DVDCOPY\_设置\_副本\_STATE 属性设置的 DVD 解码器流的副本状态。 此为可选属性来实现。
ms.assetid: f4e46d79-c70b-413a-9702-a73d3776ee2c
keywords:
- KSPROPERTY_DVDCOPY_SET_COPY_STATE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_DVDCOPY_SET_COPY_STATE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6cbf46f5fe0848e4ed24efb4cfb06b1e9ca566b8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555739"
---
# <a name="kspropertydvdcopysetcopystate"></a>KSPROPERTY\_DVDCOPY\_SET\_COPY\_STATE


KSPROPERTY\_DVDCOPY\_设置\_副本\_STATE 属性设置的 DVD 解码器流的副本状态。 此为可选属性来实现。

## <span id="ddk_ksproperty_dvdcopy_set_copy_state_ks"></span><span id="DDK_KSPROPERTY_DVDCOPY_SET_COPY_STATE_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567639" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_SET_COPY_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567639)"><strong>KS_DVDCOPY_SET_COPY_STATE</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KS\_DVDCOPY\_设置\_副本\_状态结构描述的 DVD 解码器流版权保护状态。

<a name="remarks"></a>备注
-------

此属性指示此 pin 是否需要 CSS 身份验证。 如果未实现该属性，默认值假定**KS\_DVDCOPYSTATE\_身份验证\_必需**值从[ **KS\_DVDCOPYSTATE** ](https://msdn.microsoft.com/library/windows/hardware/ff567634)枚举。

此属性的主要用途是为支持多个具有相同的解密器 pin 的解码器。 例如，如果子画面和视频解码，提供了一个筛选器，密钥只需一个两个 pin 进行交换。 如果筛选器函数将返回**KS\_DVDCOPYSTATE\_身份验证\_不\_REQUIRED**上其中一个球瓶，则它必须始终返回**KS\_DVDCOPYSTATE\_身份验证\_必需**上发出该属性的第一个 pin。

当此属性作为发出**获取**调用中，筛选器可以响应使用**KS\_DVDCOPYSTATE\_身份验证\_必需**或 KS\_DVDCOPYSTATE\_身份验证\_不\_必需。

当此属性作为发出**设置**调用时，这是硬件解码器用于指示要输入哪些阶段版权保护协商一条信息性调用。 解码器可以保存一组关闭\_直到已接收到的正确位，指示新的 CSS 密钥必需的具有下列任一状态：

<span id="KS_DVDCOPYSTATE_INITIALIZE"></span><span id="ks_dvdcopystate_initialize"></span>**KS\_DVDCOPYSTATE\_INITIALIZE**  
指示光盘的密钥协商序列的开头。

<span id="KS_DVDCOPYSTATE_INITIALIZE_TITLE"></span><span id="ks_dvdcopystate_initialize_title"></span>**KS\_DVDCOPYSTATE\_INITIALIZE\_TITLE**  
指示标题的密钥协商序列的开头。

<span id="KS_DVDCOPYSTATE_DONE"></span><span id="ks_dvdcopystate_done"></span>**KS\_DVDCOPYSTATE\_DONE**  
指示密钥协商序列完成。

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


[**KS\_DVDCOPY\_SET\_COPY\_STATE**](https://msdn.microsoft.com/library/windows/hardware/ff567639)

[**KS\_DVDCOPYSTATE**](https://msdn.microsoft.com/library/windows/hardware/ff567634)

[DVD 版权保护](https://msdn.microsoft.com/library/windows/hardware/ff558736)

[在同一硬件上的多个数据流](https://msdn.microsoft.com/library/windows/hardware/ff567744)

[与数据流同步密钥交换](https://msdn.microsoft.com/library/windows/hardware/ff568511)

 

 






