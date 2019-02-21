---
title: KsTimedFilterCallbacks 规则 （)
description: KsTimedFilterCallbacks 规则指定一个内核流式处理 (KS) 微型端口驱动程序返回从 500 毫秒内的某个筛选器回调函数。
ms.assetid: 5F631D49-405F-4F1A-A280-FEFB4ADA460D
ms.date: 05/21/2018
keywords:
- KsTimedFilterCallbacks 规则 （)
topic_type:
- apiref
api_name:
- KsTimedFilterCallbacks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f9144b7a72b86fe1d3a75473ece4ef3c7f2f4994
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521176"
---
# <a name="kstimedfiltercallbacks-rule-"></a>KsTimedFilterCallbacks 规则 （)


KsTimedFilterCallbacks 规则指定一个内核流式处理 (KS) 微型端口驱动程序返回从 500 毫秒内的某个筛选器回调函数。

|              |     |
|--------------|-----|
| 驱动程序模型 | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00082003) |

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

 

 

 





