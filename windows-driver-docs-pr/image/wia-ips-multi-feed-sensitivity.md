---
title: WIA\_IPS\_多\_馈送\_敏感度
description: WIA\_IPS\_多\_馈送\_敏感度属性用于将多源的检测触发器更改为较低或更高版本的设备支持的最低和最高敏感度介于。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 04AC211B-89D5-417F-9089-1E3F30E22211
keywords:
- WIA_IPS_MULTI_FEED_SENSITIVITY 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_MULTI_FEED_SENSITIVITY
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81709afe5d496b731b495d8195b1e28eb4c4df16
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546119"
---
# <a name="wiaipsmultifeedsensitivity"></a>WIA\_IPS\_多\_馈送\_敏感度


**WIA\_IPS\_多\_源\_敏感度**属性用于将多源的检测触发器更改为较低或更高版本的最低和最高敏感度介于支持的设备。 WIA 微型驱动程序创建并维护此属性。




属性类型：VT\_I4

有效值：WIA\_PROP\_RANGE

访问权限：读/写

<a name="remarks"></a>备注
-------

此属性是可选的并且仅对送纸器数据源项有效 (以表示[ **WIA\_IPA\_项\_类别**](wia-ipa-item-category.md)属性作为 WIA\_类别\_送纸器) 时[ **WIA\_IP\_多\_源**](wia-ips-multi-feed.md)除了 WIA至少一个其他值与支持\_多\_馈送\_检测\_已禁用。

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
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





