---
title: KsFilterMutex 规则（）
description: KsFilterMutex 规则指定一个 KS 微型端口驱动程序获取并按正确的顺序释放筛选器互斥体。
ms.assetid: 09927C42-2F05-49F6-AFE1-E45049ED2805
ms.date: 05/21/2018
keywords:
- KsFilterMutex 规则（）
topic_type:
- apiref
api_name:
- KsFilterMutex
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d7dc2bb65b2096f128516136c89bff01f484820d
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968098"
---
# <a name="ksfiltermutex-rule-"></a>KsFilterMutex 规则（）


KsFilterMutex 规则指定一个 KS 微型端口驱动程序获取并按正确的顺序释放筛选器互斥体。

-   KS 微型端口驱动程序无法以递归方式获取筛选器互斥体。
-   线程不应在不首先获取筛选器互斥体的情况下将其释放。

**驱动程序模型： KS**

**找到了具有此规则的 bug 检查**： [**bug 检查0XC4：驱动程序 \_ 验证程序 \_ 检测到 \_ 冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)（0x0008100A）


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
<td align="left"><p>若要验证此规则，请打开 "命令提示符" 窗口。 输入 Driver Verifier 命令并指定<strong>/domain ks</strong>。</p>
<p>例如：</p>
<p></p>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

 

**验证程序/domain ks** \[*选项* \]**/driver** * &lt; yourdriver &gt; *另请参阅
--------

[AVStream 中的筛选器控件互斥](https://docs.microsoft.com/windows-hardware/drivers/stream/filter-control-mutex-in-avstream)
 

 





