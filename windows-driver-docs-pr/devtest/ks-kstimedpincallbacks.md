---
title: 'KsTimedPinCallbacks 规则 ( # A1'
description: KsTimedPinCallbacks 规则指定内核流式处理 (KS) 微型端口驱动程序在 500 ms 内从 pin 回调函数返回。
ms.date: 05/21/2018
keywords:
- 'KsTimedPinCallbacks 规则 ( # A1'
topic_type:
- apiref
api_name:
- KsTimedPinCallbacks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b06fd60c2a65e7bb4e2a7b6181ca2bd8ea9d7b8a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830199"
---
# <a name="kstimedpincallbacks-rule-"></a>KsTimedPinCallbacks 规则 ( # A1


KsTimedPinCallbacks 规则指定内核流式处理 (KS) 微型端口驱动程序在 500 ms 内从 pin 回调函数返回。

**驱动程序模型： KS**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0x00082004) 


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

 

