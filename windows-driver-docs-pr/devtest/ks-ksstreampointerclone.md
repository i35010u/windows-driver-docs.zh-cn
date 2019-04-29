---
title: KsStreamPointerClone 规则 （)
description: KsStreamPointerClone 规则指定内核流 (KS) 微型端口驱动程序正确使用 KsStreamPointerClone 和 KsStreamPointerDelete 函数。
ms.assetid: 5ECF0070-0E36-4A91-B9FA-AA0DB7636B0E
ms.date: 05/21/2018
keywords:
- KsStreamPointerClone 规则 （)
topic_type:
- apiref
api_name:
- KsStreamPointerClone
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 014522055a90d46e203b6c6abbd3113d22418654
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364707"
---
# <a name="ksstreampointerclone-rule-"></a>KsStreamPointerClone 规则 （)


KsStreamPointerClone 规则指定内核流 (KS) 微型端口驱动程序正确使用[ **KsStreamPointerClone** ](https://msdn.microsoft.com/library/windows/hardware/ff567129)并[ **KsStreamPointerDelete**](https://msdn.microsoft.com/library/windows/hardware/ff567130)函数。

|              |     |
|--------------|-----|
| 驱动程序模型 | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00081002) |

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

 

 

 





