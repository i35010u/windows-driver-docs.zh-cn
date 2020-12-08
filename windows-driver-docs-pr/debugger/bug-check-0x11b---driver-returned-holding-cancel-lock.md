---
title: Bug 检查 0x11B DRIVER_RETURNED_HOLDING_CANCEL_LOCK
description: DRIVER_RETURNED_HOLDING_CANCEL_LOCK bug 检查的值为0x0000011B。
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
ms.openlocfilehash: 3449a739b44335fdb751cf5061233ea23ce1f225
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816973"
---
# <a name="bug-check-0x11b-driver_returned_holding_cancel_lock"></a>Bug 检查0x11B：驱动程序 \_ 返回了 \_ 保留 \_ 取消 \_ 锁定


驱动程序 \_ 返回 \_ 保存 \_ 取消 \_ 锁定 bug 检查的值为0x0000011B。 此 bug 检查表明驱动程序已从保存全局取消锁定的 *cancel* 例程中返回。 这会导致以后的所有取消调用失败，并导致死锁或其他 bug 检查。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="driver_returned_holding_cancel_lock-parameters"></a>驱动程序 \_ 返回了 \_ 包含 \_ 取消 \_ 锁定参数


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
<td align="left"><p> (取消的 IRP 的地址在) 中可能无效。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p><em>取消</em>例程的地址。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

取消旋转锁定应已由 *取消* 例程释放。

驱动程序调用 IoCancelIrpIoCancelIrp 函数来取消单个 i/o 请求数据包 (IRP) 。 此函数获取 cancel 自旋锁，在 IRP 中设置 cancel 标志，然后，如果指定了例程，则调用 IRP 中相应字段指定的 *取消* 例程。 需要 *取消* 例程才能释放取消自旋锁。 如果没有 *取消* 例程，则释放 "取消旋转" 锁。

 

 




