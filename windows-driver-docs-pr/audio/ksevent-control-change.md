---
title: KSEVENT\_控制\_更改
description: KSEVENT\_控制\_更改事件指示控件值的更改发生在表示硬件音量控制旋钮、 静音开关或手动控制其他类型的节点。使用情况摘要 TableTargetEvent 描述符 TypeEvent 值 TypePinKSE\_NODEKSEVENTDATA 事件值类型 （操作数据） 是一种 KSEVENTDATA 结构，指定要对某个事件使用的通知类型。
ms.assetid: 32d8e14c-f21d-4bac-8d98-8aca40e30b60
keywords:
- KSEVENT_CONTROL_CHANGE 音频设备
topic_type:
- apiref
api_name:
- KSEVENT_CONTROL_CHANGE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 076d3e98ef978315ea4ef1955c2b7a90f0f8e1ee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548164"
---
# <a name="kseventcontrolchange"></a>KSEVENT\_控制\_更改


KSEVENT\_控制\_更改事件指示控件值的更改发生在表示硬件音量控制旋钮、 静音开关或手动控制其他类型的节点。

**使用率摘要表**

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">目标</th>
<th align="left">事件描述符类型</th>
<th align="left">事件值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561937" data-raw-source="[&lt;strong&gt;KSE_NODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561937)"><strong>KSE_NODE</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561750" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561750)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

事件值类型 （操作数据） 是通知的 KSEVENTDATA 结构，它指定要对某个事件使用类型。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSE\_NODE**](https://msdn.microsoft.com/library/windows/hardware/ff561937)

[**KSEVENTDATA**](https://msdn.microsoft.com/library/windows/hardware/ff561750)

[**PCEVENT\_项**](https://msdn.microsoft.com/library/windows/hardware/ff537692)

[**PCEVENT\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff537693)

[IPortEvents](https://msdn.microsoft.com/library/windows/hardware/ff536884)

 

 






