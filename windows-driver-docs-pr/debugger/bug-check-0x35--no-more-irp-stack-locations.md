---
title: Bug 检查 0x35 NO_MORE_IRP_STACK_LOCATIONS
description: NO_MORE_IRP_STACK_LOCATIONS bug 检查具有 0x00000035 值。 IoCallDriver 数据包已没有更多剩余的堆栈位置时发生此 bug 检查。
ms.assetid: 1a8d5a1b-70aa-4846-bafe-0fef041570c1
keywords:
- Bug 检查 0x35 NO_MORE_IRP_STACK_LOCATIONS
- NO_MORE_IRP_STACK_LOCATIONS
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- NO_MORE_IRP_STACK_LOCATIONS
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 96de449039449fa2559afb053e625e53ccb22e05
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519642"
---
# <a name="bug-check-0x35-nomoreirpstacklocations"></a>Bug 检查 0x35:否\_更多\_IRP\_堆栈\_位置


否\_更多\_IRP\_堆栈\_位置错误检查的值为 0x00000035。 检查此错误发生时**IoCallDriver**数据包已没有更多剩余的堆栈位置。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="nomoreirpstacklocations-parameters"></a>否\_更多\_IRP\_堆栈\_位置参数


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
<td align="left"><p>IRP 的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

更高级别的驱动程序已尝试调用的较低级驱动程序通过**IoCallDriver**接口，但有没有更多的堆栈位置数据包中。 这将阻止较低级别驱动程序访问其参数。

这是灾难性的情况下，因为更高级别驱动程序将继续执行，因为如果它已填写 （根据需要） 较低级别的驱动程序的参数。 但由于没有后一种驱动程序的堆栈位置，前者具有实际写入数据包的末尾。 这意味着某些其他内存已以及损坏。

 

 




