---
title: 'KsStreamPointerUnlock 规则 ( # A1'
description: KsStreamPointerUnlock 规则指定内核流式处理 (KS) 微型端口驱动程序在卸载驱动程序之前解锁所有流指针 (或) 设备停止。
ms.assetid: 74742111-85C2-44D2-ACDB-BE1D2D468ED5
ms.date: 05/21/2018
keywords:
- 'KsStreamPointerUnlock 规则 ( # A1'
topic_type:
- apiref
api_name:
- KsStreamPointerUnlock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 205190996460e384092ef5d0f7f2b0f55dcc614d
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382349"
---
# <a name="ksstreampointerunlock-rule-"></a>KsStreamPointerUnlock 规则 ( # A1


KsStreamPointerUnlock 规则指定内核流式处理 (KS) 微型端口驱动程序在卸载驱动程序之前解锁所有流指针 (或) 设备停止。

**驱动程序模型： KS**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0x00081004) 


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

 

 

