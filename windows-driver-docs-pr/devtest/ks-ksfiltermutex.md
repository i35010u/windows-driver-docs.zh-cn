---
title: KsFilterMutex 规则 （)
description: KsFilterMutex 规则指定 KS 微型端口驱动程序获取并释放该筛选器互斥体以正确的顺序。
ms.assetid: 09927C42-2F05-49F6-AFE1-E45049ED2805
ms.date: 05/21/2018
keywords:
- KsFilterMutex 规则 （)
topic_type:
- apiref
api_name:
- KsFilterMutex
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6bd5dadbff6d84016b218665f33b255faa715162
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374701"
---
# <a name="ksfiltermutex-rule-"></a>KsFilterMutex 规则 （)


KsFilterMutex 规则指定 KS 微型端口驱动程序获取并释放该筛选器互斥体以正确的顺序。

-   KS 微型端口驱动程序无法获取筛选器的互斥体以递归方式。
-   线程应释放而无需首先获取筛选器互斥体。

|              |     |
|--------------|-----|
| 驱动程序模型 | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x0008100A) |

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
<p></p>
<p>有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

 

**验证程序 /domain ks** \[*选项*\] **/driver** *&lt;yourdriver&gt;* 另请参阅
--------

[筛选器控件中 AVStream 的互斥体](https://msdn.microsoft.com/library/windows/hardware/ff559603)
 

 





