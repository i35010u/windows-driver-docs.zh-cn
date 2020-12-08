---
title: Bug 检查 0xBFE BC_BLUETOOTH_VERIFIER_FAULT
description: BC_BLUETOOTH_VERIFIER_FAULT bug 检查的值为0x00000BFE。 这表明驱动程序导致了冲突。
keywords:
- Bug 检查 0xBFE BC_BLUETOOTH_VERIFIER_FAULT
- BC_BLUETOOTH_VERIFIER_FAULT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- BC_BLUETOOTH_VERIFIER_FAULT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 070973d3f9dfa5d0346cfada1d515401321348ab
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783541"
---
# <a name="bug-check-0xbfe-bc_bluetooth_verifier_fault"></a>Bug 检查0xBFE： BC \_ 蓝牙 \_ 验证程序 \_ 错误


BC \_ 蓝牙 \_ 验证程序 \_ 错误检查的值为0x00000BFE。 这表明驱动程序导致了冲突。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="bc_bluetooth_verifier_fault-parameters"></a>BC \_ 蓝牙 \_ 验证程序 \_ 错误参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">1</td>
<td align="left"><p>蓝牙验证程序错误的子类型。</p>
<div class="code">
<code>0x1 : An attempt was made to submit a Bluetooth Request Block that is already in use
                  2 - Brb pointer
                  3 - Reserved
                  4 - Reserved
            0x2 : An attempt was made to free a Bluetooth Request Block that is in use
                  2 - Brb pointer
                  3 - Reserved
                  4 - Reserved
            0x3 : An attempt was made to allocate or initialize an invalid BRB type
                  2 - Brb pointer
                  3 - pdo extension (if available)
                  4 - Reserved
            0x4 : Invalid Bluetooth Request Block pointer was submitted
                  2 - Brb pointer
                  3 - Reserved
                  4 - Reserved
            0x5 : A Bluetooth Request Block with an invalid size was submitted
                  2 - Brb pointer
                  3 - Actual Size
                  4 - Expected Size
            0x6 : The IOCTL_BTH_GET_DEVICE_INFO was called with invalid parameters
                  2 - Reserved
                  3 - Reserved
                  4 - Reserved
            0x7 : BRB_L2CA_UNREGISTER_SERVER was submitted with an invalid server handle
                  2 - Server handle
                  3 - Reserved
                  4 - Reserved
            0x8 : BRB_L2CA_CLOSE_CHANNEL was submitted with an invalid channel handle
                  2 - Brb pointer
                  3 - Channel handle
                  4 - Reserved
            0x9 : BRB_SCO_UNREGISTER_SERVER was submitted with an invalid server handle
                  2 - Server handle
                  3 - Reserved
                  4 - Reserved</code>
</div></td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">请参阅参数1</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">请参阅参数1</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">请参阅参数1</td>
</tr>
</tbody>
</table>



<a name="resolution"></a>解决方法
----------

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。
参数1描述了冲突类型。 查看调用堆栈，确定驱动程序是否有异常。








