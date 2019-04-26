---
title: Bug 检查 0x44 MULTIPLE_IRP_COMPLETE_REQUESTS
description: MULTIPLE_IRP_COMPLETE_REQUESTS bug 检查具有 0x00000044 值。 这指示一个驱动程序已尝试请求，它是完成 IRP 已经完成。
ms.assetid: bc60b4b3-aded-4c67-bbaa-aad1b6b38d30
keywords:
- Bug 检查 0x44 MULTIPLE_IRP_COMPLETE_REQUESTS
- MULTIPLE_IRP_COMPLETE_REQUESTS
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- MULTIPLE_IRP_COMPLETE_REQUESTS
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8092ad90ad412de72c1d72510c27358b6c421640
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325369"
---
# <a name="bug-check-0x44-multipleirpcompleterequests"></a>Bug 检查 0x44：多个\_IRP\_完成\_请求


多个\_IRP\_完成\_请求错误检查的值为 0x00000044。 这指示一个驱动程序已尝试请求，它是完成 IRP 已经完成。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="multipleirpcompleterequests-parameters"></a>多个\_IRP\_完成\_请求参数


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

驱动程序已调用**IoCompleteRequest**询问，完成 IRP，但已完成数据包。

<a name="resolution"></a>分辨率
----------

这是一个棘手的 bug 地发现，因为最简单的情况-尝试两次完成其自己的数据包的驱动程序-不通常是问题根源。 更有可能，两个单独的驱动程序每个认为他们所拥有数据包，并且每个已尝试完成它。 第一个请求成功，而第二个失败了，从而导致此 bug 检查。

跟踪系统中的驱动程序导致了错误是很困难，因为跟踪的第一个驱动程序已介绍第二个。 但是，可以通过检查设备对象字段在每个堆栈位置中的找到当前请求的驱动程序堆栈。

 

 




