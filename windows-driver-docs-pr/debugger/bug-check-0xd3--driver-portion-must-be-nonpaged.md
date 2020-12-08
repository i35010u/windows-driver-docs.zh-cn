---
title: Bug 检查 0xD3 DRIVER_PORTION_MUST_BE_NONPAGED
description: DRIVER_PORTION_MUST_BE_NONPAGED bug 检查的值为0x000000D3。 这表示系统尝试在进程 IRQL 上访问分页内存过高的情况。
keywords:
- Bug 检查 0xD3 DRIVER_PORTION_MUST_BE_NONPAGED
- DRIVER_PORTION_MUST_BE_NONPAGED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_PORTION_MUST_BE_NONPAGED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2f094d50ee423f637d5f14684fe1b214f38ea81a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802001"
---
# <a name="bug-check-0xd3-driver_portion_must_be_nonpaged"></a>Bug 检查0xD3：驱动程序 \_ 部分 \_ 必须未 \_ \_ 分页


驱动程序 \_ 部分 \_ 必须 \_ 为 " \_ 非分页 bug 检查" 的值为 "0x000000D3"。 这表示系统尝试在进程 IRQL 上访问分页内存过高的情况。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="driver_portion_must_be_nonpaged-parameters"></a>驱动程序 \_ 部分 \_ 必须 \_ 为 \_ 非分页参数


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
<td align="left"><p>引用的内存</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>引用时为 IRQL</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>0：</strong> 读取</p>
<p><strong>1：</strong> 写入</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>对引用的内存进行寻址</p></td>
</tr>
</tbody>
</table>

 

如果能够识别出导致错误的驱动程序，则其名称将打印在蓝屏上，并存储在内存中的 (PUNICODE\_STRING) KiBugCheckDriver  位置。

<a name="cause"></a>原因
-----

此 bug 检查通常是由未正确地将自己的代码或数据标记为可分页的驱动程序引起的。

<a name="resolution"></a>解决方法
----------

若要开始调试，请使用内核调试器获取堆栈跟踪： [**！分析**](-analyze.md) 调试扩展显示有关 bug 检查的信息，可帮助确定根本原因，然后使用 [**Kb (显示 stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)  命令获取堆栈跟踪。

 

 




