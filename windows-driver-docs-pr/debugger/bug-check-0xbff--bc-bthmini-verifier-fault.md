---
title: Bug 检查 0xBFF BC_BTHMINI_VERIFIER_FAULT
description: BC_BTHMINI_VERIFIER_FAULT bug 检查的值为0x00000BFF。 这表明蓝牙微型端口可扩展驱动程序验证程序已捕获到冲突。
keywords:
- Bug 检查 0xBFF BC_BTHMINI_VERIFIER_FAULT
- BC_BTHMINI_VERIFIER_FAULT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- BC_BTHMINI_VERIFIER_FAULT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f2ba7bb612c975e619dc3019027a4d135ffb20b2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783533"
---
# <a name="bug-check-0xbff-bc_bthmini_verifier_fault"></a>Bug 检查0xBFF： BC \_ BTHMINI \_ 验证程序 \_ 错误


BC \_ BTHMINI \_ VERIFIER \_ 错误检查的值为0x00000BFF。 这表明蓝牙微型端口可扩展驱动程序验证程序已捕获到冲突。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="bc_bthmini_verifier_fault-parameters"></a>BC \_ BTHMINI \_ 验证程序 \_ 错误参数


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
<code>0x1 : An attempt was made to return a packet with type that mis-matched its original request.
                  2 - Returned packet type
                  3 - Expected packet type
                  4 - Reserved
            0x2 : An attempt was made to return an unexpected status code and caused the packet to be discarded.
                  2 - Unexpected return status
                  3 - Reserved
                  4 - Reserved
            0x3 : Incorrect output buffer size was returned to indicate number of bytes written by the lower transport driver.
                  2 - Unexpected buffer size
                  3 - Expected buffer size
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








