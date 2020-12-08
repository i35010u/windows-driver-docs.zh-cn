---
title: Bug 检查 0x4A IRQL_GT_ZERO_AT_SYSTEM_SERVICE
description: IRQL_GT_ZERO_AT_SYSTEM_SERVICE bug 检查的值为0x0000004A。 这表示当线程仍在 PASSIVE_LEVEL 时，线程将从系统调用返回到用户模式。
keywords:
- Bug 检查 0x4A IRQL_GT_ZERO_AT_SYSTEM_SERVICE
- IRQL_GT_ZERO_AT_SYSTEM_SERVICE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- IRQL_GT_ZERO_AT_SYSTEM_SERVICE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 730f74c976db05b99907b4a75298eac93e32575c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831655"
---
# <a name="bug-check-0x4a-irql_gt_zero_at_system_service"></a>Bug 检查0x4A： IRQL \_ GT \_ \_ \_ 系统服务处的零 \_


\_ \_ \_ 系统服务 bug 检查中的 IRQL GT 0 的 \_ \_ 值为0x0000004A。 这表示当某个线程的 IRQL 仍高于被动级别时，该线程从系统调用返回到用户模式 \_ 。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="irql_gt_zero_at_system_service-parameters"></a>IRQL \_ \_ \_ 在 \_ 系统 \_ 服务参数处为零


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
<td align="left"><p>1</p></td>
<td align="left"><p>系统函数 (系统调用例程的地址) </p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>当前 IRQL</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>


## <a name="resolution"></a>解决方法 
[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。
 

 




