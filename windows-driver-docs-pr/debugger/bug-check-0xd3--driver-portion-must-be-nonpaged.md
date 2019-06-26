---
title: Bug 检查 0xD3 DRIVER_PORTION_MUST_BE_NONPAGED
description: DRIVER_PORTION_MUST_BE_NONPAGED bug 检查具有 0x000000D3 值。 这表示系统尝试访问在过程 IRQL 过高的可分页内存。
ms.assetid: 8b33dd20-9faa-4c02-96b7-89f55e69aeec
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
ms.openlocfilehash: 6e3eef615d14d6dcc0ea5dd798f52cce2db0d4e4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361568"
---
# <a name="bug-check-0xd3-driverportionmustbenonpaged"></a>Bug 检查 0xD3：驱动程序\_部分\_必须\_BE\_未分页


该驱动程序\_部分\_必须\_BE\_非分页的错误检查的值为 0x000000D3。 这表示系统尝试访问在过程 IRQL 过高的可分页内存。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


## <a name="driverportionmustbenonpaged-parameters"></a>驱动程序\_部分\_必须\_BE\_非分页的参数


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
<td align="left"><p>在引用的时间的 IRQL</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>0:</strong>Read</p>
<p><strong>1:</strong>写入</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>引用内存的地址</p></td>
</tr>
</tbody>
</table>

 

如果无法确定导致错误的驱动程序，其名称是蓝色屏幕上输出和位置在内存中存储 (PUNICODE\_字符串) **KiBugCheckDriver**。

<a name="cause"></a>原因
-----

检查此错误通常是由其自己的代码或数据作为可分页错误地标记驱动程序引起的。

<a name="resolution"></a>分辨率
----------

若要开始调试，请使用内核调试程序获取堆栈跟踪。

 

 




