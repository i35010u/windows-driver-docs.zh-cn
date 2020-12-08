---
title: KSPROPERTY \_ DVDCOPY \_ 设置 \_ 复制 \_ 状态
description: KSPROPERTY \_ DVDCOPY \_ 设置 \_ 复制 \_ 状态属性设置 DVD 解码器流的复制状态。 此属性可用于实现。
keywords:
- KSPROPERTY_DVDCOPY_SET_COPY_STATE 流媒体设备
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
ms.openlocfilehash: 1c27efdacdd490ace92ab3db669edc1da4433e2d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795307"
---
# <a name="ksproperty_dvdcopy_set_copy_state"></a>KSPROPERTY \_ DVDCOPY \_ 设置 \_ 复制 \_ 状态


KSPROPERTY \_ DVDCOPY \_ 设置 \_ 复制 \_ 状态属性设置 DVD 解码器流的复制状态。 此属性可用于实现。

## <span id="ddk_ksproperty_dvdcopy_set_copy_state_ks"></span><span id="DDK_KSPROPERTY_DVDCOPY_SET_COPY_STATE_KS"></span>


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
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_set_copy_state" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_SET_COPY_STATE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_set_copy_state)"><strong>KS_DVDCOPY_SET_COPY_STATE</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 KS \_ DVDCOPY \_ 集 \_ 复制 \_ 状态结构，描述 DVD 解码器流的版权保护状态。

<a name="remarks"></a>备注
-------

此属性指示此 pin 是否需要 CSS 身份验证。 如果未实现该属性，则假定默认值为 ks [**\_ DVDCOPYSTATE**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ks_dvdcopystate)枚举中的 **ks \_ DVDCOPYSTATE \_ AUTHENTICATION \_ 必需** 值。

此属性的主要用途是用于支持具有相同 decrypter 的多个 pin 的解码器。 例如，如果一个筛选器同时提供了子画面和视频解码，则只需为这两个 pin 中的一个提供交换密钥。 如果筛选器将返回某个 pin **\_ \_ \_ 不 \_ 需要 ks DVDCOPYSTATE authentication** ，则必须始终在对其发出属性的第一个 pin 上返回 **ks \_ DVDCOPYSTATE \_ authentication \_** 。

当此属性作为 **Get** 调用发出时，筛选器可以使用 **\_ \_ \_ 所需的 ks DVDCOPYSTATE authentication** 或 ks \_ DVDCOPYSTATE authentication 进行响应 \_ \_ \_ 。

如果此属性作为 **集** 调用发出，则这是一个信息性调用，由硬件解码器用来指示正在输入版权保护协商的哪个阶段。 解码器可以 \_ 通过以下方式之一来保持设置状态，直到收到正确的位，指出需要新的 CSS 密钥：

<span id="KS_DVDCOPYSTATE_INITIALIZE"></span><span id="ks_dvdcopystate_initialize"></span>**KS \_ DVDCOPYSTATE \_ 初始化**  
指示光盘密钥协商序列的开头。

<span id="KS_DVDCOPYSTATE_INITIALIZE_TITLE"></span><span id="ks_dvdcopystate_initialize_title"></span>**KS \_ DVDCOPYSTATE \_ 初始化 \_ 标题**  
指示标题键协商序列的开头。

<span id="KS_DVDCOPYSTATE_DONE"></span><span id="ks_dvdcopystate_done"></span>**KS \_ DVDCOPYSTATE 已 \_ 完成**  
指示密钥协商序列的完成。

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

## <a name="see-also"></a>请参阅


[**KS \_ DVDCOPY \_ 设置 \_ 复制 \_ 状态**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_set_copy_state)

[**KS \_ DVDCOPYSTATE**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ks_dvdcopystate)

[DVD 版权保护](./dvd-copyright-protection.md)

[同一硬件上的多个数据流](./multiple-data-streams-on-the-same-hardware.md)

[将密钥交换与数据流同步](./synchronizing-key-exchange-with-data-flow.md)

