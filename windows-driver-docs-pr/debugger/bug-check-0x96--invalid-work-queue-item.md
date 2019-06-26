---
title: Bug 检查 0x96 INVALID_WORK_QUEUE_ITEM
description: INVALID_WORK_QUEUE_ITEM bug 检查具有 0x00000096 值。 此 bug 检查指示某个队列项被移除包含一个 NULL 指针。
ms.assetid: 18d7d8b2-814c-4207-aac9-e3affc2ccebd
keywords:
- Bug 检查 0x96 INVALID_WORK_QUEUE_ITEM
- INVALID_WORK_QUEUE_ITEM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INVALID_WORK_QUEUE_ITEM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e7019b28256d9f828f97c467be343b43f0886f58
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361714"
---
# <a name="bug-check-0x96-invalidworkqueueitem"></a>Bug 检查 0x96：无效\_工作\_队列\_项


无效\_工作\_队列\_项 bug 检查的值为 0x00000096。 此 bug 检查指示某个队列项被移除，包含**NULL**指针。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


## <a name="invalidworkqueueitem-parameters"></a>无效\_工作\_队列\_项参数


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
<td align="left"><p>队列项的地址的其<strong>flink</strong>或<strong>闪烁</strong>字段是<strong>NULL</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>正在引用的队列的地址。 通常情况下，此队列是<strong>ExWorkerQueue</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>基址<strong>ExWorkerQueue</strong>数组。 (此地址可帮助你确定有问题的队列是否确实<strong>ExWorkerQueue</strong>。 如果队列，则<strong>ExWorkerQueue</strong>，此参数的偏移量位置将隔离队列。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>假设队列是<strong>ExWorkerQueue</strong>，此值是将工作项有效如果已调用的工作线程例程的地址。 （您可以使用此地址来隔离误用工作队列的驱动程序。）</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

无效\_工作\_队列\_项 bug 检查发生时**KeRemoveQueue**中移除某个队列项其**flink**或**闪烁**字段是**NULL**。

队列不当使用会导致此错误。 但此错误通常是因为工作线程工作项被误用。

队列中的项可以只进行一次插入列表上。 从队列中移除项时其**flink**字段设置为**NULL**。 然后，此项目中删除时的第二个时间，都会进行此 bug 检查。

在大多数情况下，所引用的队列是**ExWorkerQueue** （执行辅助角色队列）。 为了帮助识别导致错误的驱动程序，参数 4 显示了将此工作项有效如果已调用的工作线程例程的地址。 但是，与队列是否正在引用不是**ExWorkerQueue**，此参数不是很有用。

 

 




