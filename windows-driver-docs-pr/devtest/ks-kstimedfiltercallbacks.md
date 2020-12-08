---
title: 'KsTimedFilterCallbacks 规则 ( # A1'
description: KsTimedFilterCallbacks 规则指定内核流式处理 (KS) 微型端口驱动程序在500毫秒内从筛选器回调函数返回。
ms.date: 05/21/2018
keywords:
- 'KsTimedFilterCallbacks 规则 ( # A1'
topic_type:
- apiref
api_name:
- KsTimedFilterCallbacks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c8593ea3a6125b1dfd01a93611466512d477dbdd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829949"
---
# <a name="kstimedfiltercallbacks-rule-"></a>KsTimedFilterCallbacks 规则 ( # A1


KsTimedFilterCallbacks 规则指定内核流式处理 (KS) 微型端口驱动程序在500毫秒内从筛选器回调函数返回。

**驱动程序模型： KS**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0x00082003) 


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
<td align="left"><p>若要验证此规则，请打开 "命令提示符" 窗口。 输入 Driver Verifier 命令并指定 <strong>/domain ks</strong>。</p>
<p>例如：</p>
<p><strong>验证程序/domain ks</strong> [<em>options</em>] <strong>/driver</strong> <em> &lt; &gt; yourdriver</em></p>
<p>有关详细信息，请参阅<a href="/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a>。</p></td>
</tr>
</tbody>
</table>

 

