---
title: KsStreamPointerLock 规则 （)
description: KsStreamPointerLock 规则指定一个内核流式处理 (KS) 微型端口驱动程序使用 KsStreamPointerLock 和 KsStreamPointerUnlock 函数，以正确的顺序。
ms.assetid: 365C8656-57F1-4774-9859-B67D64403BB3
ms.date: 05/21/2018
keywords:
- KsStreamPointerLock 规则 （)
topic_type:
- apiref
api_name:
- KsStreamPointerLock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 334f719996bbf8c553b2378befbddf16a09b1e60
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364702"
---
# <a name="ksstreampointerlock-rule-"></a>KsStreamPointerLock 规则 （)


KsStreamPointerLock 规则指定一个内核流式处理 (KS) 微型端口驱动程序使用[ **KsStreamPointerLock** ](https://msdn.microsoft.com/library/windows/hardware/ff567134)并[ **KsStreamPointerUnlock**](https://msdn.microsoft.com/library/windows/hardware/ff567137)正确的顺序的函数。

也就是说，微型端口驱动程序必须不尝试锁定已经锁定的流指针，或尝试解锁流指针不已锁定的。

|              |     |
|--------------|-----|
| 驱动程序模型 | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00081003) |

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
<td align="left"><p>若要验证此规则，请打开命令提示符窗口。 输入驱动程序验证程序命令，并指定<strong>/domain ks</strong>。</p>
<p>例如：</p>
<p><strong>verifier /domain ks</strong> [<em>options</em>] <strong>/driver</strong> <em>&lt;yourdriver&gt;</em></p>
<p>有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

 

 

 





