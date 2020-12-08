---
title: WIA \_ IPS \_ PRINTER \_ ENDORSER \_ 计数器
description: WIA \_ IPS \_ PRINTER \_ ENDORSER \_ 计数器属性用于配置新 WIA 应用程序会话开始时 imprinter/ENDORSER 计数器的起始值和递增步骤。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPS_PRINTER_ENDORSER_COUNTER 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_COUNTER
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: e527ed34bf1ba6a6048ca6f33fc3b0b371b7a698
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839085"
---
# <a name="wia_ips_printer_endorser_counter"></a>WIA \_ IPS \_ PRINTER \_ ENDORSER \_ 计数器


**WIA \_ IPS \_ PRINTER \_ ENDORSER \_ 计数器** 属性用于配置新 WIA 应用程序会话开始时 imprinter/ENDORSER 计数器的起始值和递增步骤。 WIA 微型驱动程序创建并维护此属性。




属性类型： VT \_ UI4

有效值： WIA 内容 \_ \_ 范围

访问权限：读/写

<a name="remarks"></a>备注
-------

**WIA \_ IPS \_ PRINTER \_ ENDORSER \_ 计数器** 属性的必需默认值为 0 (第一页) 。

范围步长值描述 printer/endorser 计数器值的增量值 (微型驱动程序在每个扫描) 的文档页之后递增此值。 此计数器步骤的用途不同，不应与通过 [**WIA \_ IPS \_ PRINTER \_ ENDORSER \_ step**](wia-ips-printer-endorser-step.md) 属性配置的步骤混淆。

此属性需要由所有 Imprinter/Endorser 数据源项支持。 值 0 (第一页) 是必需的。

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
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

 





