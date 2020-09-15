---
title: 'KsTimedDeviceCallbacks 规则 ( # A1'
description: KsTimedDeviceCallbacks 规则指定内核流式处理 (KS) 微型端口驱动程序在 500 ms 内从设备回调函数返回。
ms.assetid: 05393761-9018-4DAA-B8B5-EFEBBCDAB955
ms.date: 05/21/2018
keywords:
- 'KsTimedDeviceCallbacks 规则 ( # A1'
topic_type:
- apiref
api_name:
- KsTimedDeviceCallbacks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ff54046601e8bf5fc92a19fedcf5b683cefd3041
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104128"
---
# <a name="kstimeddevicecallbacks-rule-"></a>KsTimedDeviceCallbacks 规则 ( # A1


KsTimedDeviceCallbacks 规则指定内核流式处理 (KS) 微型端口驱动程序在 500 ms 内从设备回调函数返回。

**驱动程序模型： KS**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0x00082002) 


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

 

<a name="see-also"></a>另请参阅
--------

[锁定和解锁流指针](../stream/locking-and-unlocking-stream-pointers.md)
