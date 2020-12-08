---
title: Bug 检查 0x44 MULTIPLE_IRP_COMPLETE_REQUESTS
description: MULTIPLE_IRP_COMPLETE_REQUESTS bug 检查的值为0x00000044。 这表明驱动程序已尝试请求已完成的 IRP。
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
ms.openlocfilehash: e0d1a777413a0a2bd655859538de0e42d0ada2e3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840459"
---
# <a name="bug-check-0x44-multiple_irp_complete_requests"></a>Bug 检查0x44：多 \_ IRP \_ 完成的 \_ 请求数


多 \_ IRP " \_ 完成 \_ 请求 bug 检查" 的值为 "0x00000044"。 这表明驱动程序已尝试请求已完成的 IRP。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="multiple_irp_complete_requests-parameters"></a>多 \_ IRP \_ 完成 \_ 请求参数


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
<td align="left"><p>预留</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>预留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

驱动程序调用了 **IoCompleteRequest** ，要求 IRP 已完成，但数据包已经完成。

<a name="resolution"></a>解决方法
----------

这是一个棘手的 bug，因为最简单的情况（即尝试完成其自己的数据包的驱动程序），这通常不是问题的根源。 更有可能，两个单独的驱动程序分别相信它们拥有数据包，每个驱动程序都试图完成此包。 第一个请求成功，第二个请求失败，导致此 bug 检查。

跟踪系统中导致错误的驱动程序很困难，因为第二个驱动程序的原因已在第二个。 但是，可以通过检查每个堆栈位置中的设备对象字段来查找当前请求的驱动程序堆栈。

 

 




