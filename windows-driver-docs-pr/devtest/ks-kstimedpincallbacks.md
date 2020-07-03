---
title: KsTimedPinCallbacks 规则（）
description: KsTimedPinCallbacks 规则指定内核流式处理（KS）微型端口驱动程序在500毫秒内从 pin 回调函数返回。
ms.assetid: 7B8FF078-118F-465C-BF2F-FECF6EAC3568
ms.date: 05/21/2018
keywords:
- KsTimedPinCallbacks 规则（）
topic_type:
- apiref
api_name:
- KsTimedPinCallbacks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e297bc689fa9f0b57e8d78bb9af730f111e56d39
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917106"
---
# <a name="kstimedpincallbacks-rule-"></a>KsTimedPinCallbacks 规则（）


KsTimedPinCallbacks 规则指定内核流式处理（KS）微型端口驱动程序在500毫秒内从 pin 回调函数返回。

**驱动程序模型： KS**

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 找到了具有此规则的 Bug 检查 | [**Bug 检查0xC4：驱动程序 \_\_检测到 \_ 验证程序冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)（0x00082004） |

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
<p><strong>验证程序/domain ks</strong> [<em>options</em>] <strong>/driver</strong> <em> &lt; &gt; yourdriver</em></p>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

 

 

 





