---
title: Bug 检查 0x11B DRIVER_RETURNED_HOLDING_CANCEL_LOCK
description: DRIVER_RETURNED_HOLDING_CANCEL_LOCK bug 检查具有 0x0000011B 值。
ms.assetid: 8728dc74-cf21-490f-b3b0-1513d2310461
keywords:
- Bug 检查 0x11B DRIVER_RETURNED_HOLDING_CANCEL_LOCK
- DRIVER_RETURNED_HOLDING_CANCEL_LOCK
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_RETURNED_HOLDING_CANCEL_LOCK
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dfb7c4a82ff7a1a2159d11c5f3efeee006ae425e
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67521040"
---
# <a name="bug-check-0x11b-driverreturnedholdingcancellock"></a>Bug 检查 0x11B：驱动程序\_退回\_持有\_取消\_锁


该驱动程序\_退回\_持有\_取消\_锁错误检查的值为 0x0000011B。 此 bug 检查指示驱动程序已经从返回*取消*例程包含全局取消锁定。 这会导致所有更高版本的取消调用失败，并且结果中任意一种死锁或其他 bug 检查。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="driverreturnedholdingcancellock-parameters"></a>驱动程序\_退回\_持有\_取消\_锁参数


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
<td align="left"><p>已取消 IRP 的地址 （可能不是有效）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>地址<em>取消</em>例程。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

取消自旋锁应通过释放*取消*例程。

该驱动程序调用 IoCancelIrpIoCancelIrp 函数来取消单个的 I/O 请求数据包 (IRP)。 此函数获取取消自旋锁、 IRP 中的取消标志设置，然后调用*取消*指定 IRP 中的相应字段，如果指定了一个例程的例程。 *取消*例程应释放取消自旋锁。 如果没有任何*取消*取消自旋锁释放的例程。

 

 




