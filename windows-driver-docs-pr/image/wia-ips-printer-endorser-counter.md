---
title: WIA\_IPS\_打印机\_印记签署器\_计数器
description: WIA\_IPS\_打印机\_印记签署器\_计数器属性用于配置的起始值和新的 WIA 应用程序会话开始时递增印刷器/印记签署器计数器的步骤。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 3475A0DF-58EA-4B05-96EA-5BBE44655DB0
keywords:
- WIA_IPS_PRINTER_ENDORSER_COUNTER 成像设备
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
ms.openlocfilehash: a680fed0b15f3ff5397acb612e87b36128fdc07d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329937"
---
# <a name="wiaipsprinterendorsercounter"></a>WIA\_IPS\_打印机\_印记签署器\_计数器


**WIA\_IPS\_打印机\_印记签署器\_计数器**属性用于配置的起始值和递增印刷器/印记签署器计数器的开始处的步骤新的 WIA 应用程序会话。 WIA 微型驱动程序创建并维护此属性。




属性类型：VT\_UI4

有效值：WIA\_PROP\_RANGE

访问权限：读/写

<a name="remarks"></a>备注
-------

必需的默认值为**WIA\_IPS\_打印机\_印记签署器\_计数器**属性为 0 （第一页）。

范围的步长值描述打印机/印记签署器计数器值 （微型驱动程序获取扫描每个文档页之后增加此值） 的增量值。 此计数器步骤具有不同的用途，不应与可通过配置步骤相混淆[ **WIA\_IPS\_打印机\_印记签署器\_步骤**](wia-ips-printer-endorser-step.md)属性。

此属性时需要支持的所有印刷器/印记签署器数据源项。 值为 0 （第一页） 是必需。

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
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





