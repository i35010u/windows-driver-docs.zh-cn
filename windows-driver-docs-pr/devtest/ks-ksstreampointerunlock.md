---
title: KsStreamPointerUnlock 规则 （)
description: KsStreamPointerUnlock 规则指定一个内核流式处理 (KS) 微型端口驱动程序解锁所有流指针之前的驱动程序已卸载 （或停用设备）。
ms.assetid: 74742111-85C2-44D2-ACDB-BE1D2D468ED5
ms.date: 05/21/2018
keywords:
- KsStreamPointerUnlock 规则 （)
topic_type:
- apiref
api_name:
- KsStreamPointerUnlock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d8e4d3bd20c0fac35f98bfefe221039a3c9210a0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364701"
---
# <a name="ksstreampointerunlock-rule-"></a>KsStreamPointerUnlock 规则 （)


KsStreamPointerUnlock 规则指定一个内核流式处理 (KS) 微型端口驱动程序解锁所有流指针之前的驱动程序已卸载 （或停用设备）。

|              |     |
|--------------|-----|
| 驱动程序模型 | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00081004) |

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

 

 

 





