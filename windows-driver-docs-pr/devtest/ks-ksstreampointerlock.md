---
title: 'KsStreamPointerLock 规则 ( # A1'
description: KsStreamPointerLock 规则指定内核流式处理 (KS) 微型端口驱动程序在正确的序列中使用 KsStreamPointerLock 和 KsStreamPointerUnlock 函数。
ms.assetid: 365C8656-57F1-4774-9859-B67D64403BB3
ms.date: 05/21/2018
keywords:
- 'KsStreamPointerLock 规则 ( # A1'
topic_type:
- apiref
api_name:
- KsStreamPointerLock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a0068dbb2c7a2517517eefef54f94e31ebbc53e5
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382347"
---
# <a name="ksstreampointerlock-rule-"></a>KsStreamPointerLock 规则 ( # A1


KsStreamPointerLock 规则指定内核流式处理 (KS) 微型端口驱动程序在正确的序列中使用 [**KsStreamPointerLock**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerlock) 和 [**KsStreamPointerUnlock**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerunlock) 函数。

也就是说，微型端口驱动程序不得尝试锁定已锁定的流指针，或者尝试解锁尚未锁定的流指针。

**驱动程序模型： KS**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0x00081003) 


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
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a>。</p></td>
</tr>
</tbody>
</table>

 

 

