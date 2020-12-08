---
title: Bug 检查 0x48 CANCEL_STATE_IN_COMPLETED_IRP
description: CANCEL_STATE_IN_COMPLETED_IRP bug 检查的值为0x00000048。 这表明 (IRP) 的 i/o 请求包已完成，然后将其取消。
keywords:
- Bug 检查 0x48 CANCEL_STATE_IN_COMPLETED_IRP
- CANCEL_STATE_IN_COMPLETED_IRP
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CANCEL_STATE_IN_COMPLETED_IRP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fc272b73ef8e9fa41004d34a45dbc28c6ddb295e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831665"
---
# <a name="bug-check-0x48-cancel_state_in_completed_irp"></a>Bug 检查0x48： \_ \_ \_ 已完成 IRP 中的取消状态 \_


\_ \_ \_ 已完成 \_ IRP bug 检查中的 "取消" 状态的值为 "0x00000048"。 这表明 (IRP) 的 i/o 请求包已完成，然后将其取消。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="cancel_state_in_completed_irp-parameters"></a>\_ \_ \_ 已完成 \_ IRP 参数中的取消状态


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
<td align="left"><p>指向 IRP 的指针</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>驱动程序设置的取消例程</p></td>
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

具有 *取消* 例程集的 IRP 已正常完成，无需取消。 但在完成后，会出现一个名为 IRP 的 *Cancel* 例程的驱动程序。

这可能是由完成 IRP 的驱动程序导致的，然后尝试取消该驱动程序。

这也可能是由于两个驱动程序尝试以不正确的方式访问同一 IRP 而导致的。

<a name="resolution"></a>解决方法
----------

Cancel 例程参数可用于确定导致 bug 检查的驱动程序或堆栈。

 

 




