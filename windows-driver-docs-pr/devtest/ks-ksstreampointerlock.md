---
title: KsStreamPointerLock 规则（）
description: KsStreamPointerLock 规则指定内核流式处理（KS）微型端口驱动程序按正确的顺序使用 KsStreamPointerLock 和 KsStreamPointerUnlock 函数。
ms.assetid: 365C8656-57F1-4774-9859-B67D64403BB3
ms.date: 05/21/2018
keywords:
- KsStreamPointerLock 规则（）
topic_type:
- apiref
api_name:
- KsStreamPointerLock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ddd7849cacceec25e981da764a06df50d3759f3e
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916760"
---
# <a name="ksstreampointerlock-rule-"></a>KsStreamPointerLock 规则（）


KsStreamPointerLock 规则指定内核流式处理（KS）微型端口驱动程序按正确的顺序使用[**KsStreamPointerLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerlock)和[**KsStreamPointerUnlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerunlock)函数。

也就是说，微型端口驱动程序不得尝试锁定已锁定的流指针，或者尝试解锁尚未锁定的流指针。

**驱动程序模型： KS**

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 找到了具有此规则的 Bug 检查 | [**Bug 检查0xC4：驱动程序 \_\_检测到 \_ 验证程序冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)（0x00081003） |

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

 

 

 





