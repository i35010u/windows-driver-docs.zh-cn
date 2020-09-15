---
title: 'KsDeviceMutex 规则 ( # A1'
description: KsDeviceMutex 规则指定内核流式处理端口驱动程序在正确的序列中使用 KsAcquireDevice 和 KsReleaseDevice。 也就是说，每次调用 KsAcquireDevice 时，都必须具有对 KsReleaseDevice 的相应调用。
ms.assetid: 6F69B273-6780-4A01-8266-2B056E4F2C84
ms.date: 05/21/2018
keywords:
- 'KsDeviceMutex 规则 ( # A1'
topic_type:
- apiref
api_name:
- KsDeviceMutex
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 98130613ee10d191e7d65b2475d5f416b400e4c3
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105498"
---
# <a name="ksdevicemutex-rule-"></a>KsDeviceMutex 规则 ( # A1


**KsDeviceMutex**规则指定内核流式处理端口驱动程序在正确的序列中使用[**KsAcquireDevice**](/windows-hardware/drivers/ddi/ks/nf-ks-ksacquiredevice)和[**KsReleaseDevice**](/windows-hardware/drivers/ddi/ks/nf-ks-ksreleasedevice) 。 也就是说，每次调用 **KsAcquireDevice** 时，都必须具有对 **KsReleaseDevice**的相应调用。

**驱动程序模型： KS**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0x00081001) 


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

 

