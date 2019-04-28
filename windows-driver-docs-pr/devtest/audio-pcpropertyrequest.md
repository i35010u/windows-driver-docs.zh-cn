---
title: PcPropertyRequest 规则 （音频）
description: PcPropertyRequest 规则指定 PortCls 微型端口驱动程序应永远不会调用与状态的 NtStatus 值 PcCompletePendingPropertyRequest\_PENDING。
ms.assetid: 7D06F924-512F-4D21-98CD-B9E60CC8A6AB
ms.date: 05/21/2018
keywords:
- PcPropertyRequest 规则 （音频）
topic_type:
- apiref
api_name:
- PcPropertyRequest
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c0f552ae223841a10520ce2a6bba689dd9952bb8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343143"
---
# <a name="pcpropertyrequest-rule-audio"></a>PcPropertyRequest 规则 （音频）


PcPropertyRequest 规则指定 PortCls 微型端口驱动程序应永远不会调用[ **PcCompletePendingPropertyRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff537687)与*NtStatus*状态的值\_PENDING。

|              |       |
|--------------|-------|
| 驱动程序模型 | Audio |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00071008) |

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在运行时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>若要验证此规则，请打开命令提示符窗口。 输入驱动程序验证程序命令，并指定<strong>/domain 音频</strong>。</p>
<p>例如：</p>
<p><strong>verifier /domain audio</strong> [<em>options</em>] <strong>/driver</strong> <em>&lt;yourdriver&gt;</em></p>
<p>有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

 

 

 





