---
title: Bug 检查 0xC8 IRQL_UNEXPECTED_VALUE
description: IRQL_UNEXPECTED_VALUE bug 检查具有 0x000000C8 值。 这表示处理器的 IRQL 不应在此时间。
ms.assetid: eff166ab-e245-48ea-ab9e-9bb722814acf
keywords:
- Bug 检查 0xC8 IRQL_UNEXPECTED_VALUE
- IRQL_UNEXPECTED_VALUE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- IRQL_UNEXPECTED_VALUE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 02619be54eb7e7ea3b9c1fb0587c01155ba4f4a9
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903015"
---
# <a name="bug-check-0xc8-irqlunexpectedvalue"></a>Bug 检查 0xC8：IRQL\_UNEXPECTED\_VALUE


IRQL\_意外的\_值 bug 检查的值为 0x000000C8。 这表示处理器的 IRQL 不应在此时间。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="irqlunexpectedvalue-parameters"></a>IRQL\_意外的\_值参数


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
<td align="left"><p>以下位计算的值：</p>
<p>(Current IRQL &lt;&lt; 16) | (Expected IRQL &lt;&lt; 8) | UniqueValue</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>零，或<strong>APC-&gt;KernelRoutine</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>零，或<strong>APC</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>零，或<strong>APC-&gt;NormalRoutine</strong></p></td>
</tr>
</tbody>
</table>

 

您可以通过计算 （参数 1 和 0xFF） 来确定"UniqueValue"。 如果"UniqueValue"是零个或一个，参数 2、 参数 3 和参数 4 将等于所指示的 APC 指针。 否则，这些参数将等于零。

<a name="cause"></a>原因
-----

此错误通常是由设备驱动程序或一段时间内更改的 IRQL 和不能在该时间段的末尾还原原始的 IRQL 的另一个较低级别程序引起的。 例如，该例程可能已获取旋转锁并无法释放它。

 

 




