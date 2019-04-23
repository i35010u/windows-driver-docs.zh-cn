---
title: Bug 检查 0x153 KERNEL_LOCK_ENTRY_LEAKED_ON_THREAD_TERMINATION
description: KERNEL_LOCK_ENTRY_LEAKED_ON_THREAD_TERMINATION bug 检查具有 0x00000153 值。 这表示它已释放其所有 AutoBoost 锁定项之前，已终止线程。
ms.assetid: 0837C084-DAB8-4064-903D-10CD5CDE65E5
keywords:
- Bug 检查 0x153 KERNEL_LOCK_ENTRY_LEAKED_ON_THREAD_TERMINATION
- KERNEL_LOCK_ENTRY_LEAKED_ON_THREAD_TERMINATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KERNEL_LOCK_ENTRY_LEAKED_ON_THREAD_TERMINATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f6b918d60462c13c535b80c28750cce4a0f51180
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902230"
---
# <a name="bug-check-0x153-kernellockentryleakedonthreadtermination"></a>Bug 检查 0x153：内核\_锁\_条目\_已泄漏\_ON\_线程\_终止


内核\_锁\_条目\_已泄漏\_ON\_线程\_终止 bug 检查的值为 0x00000153。 这表示它已释放其所有 AutoBoost 锁定项之前，已终止线程。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="kernellockentryleakedonthreadtermination-parameters"></a>内核\_锁\_条目\_已泄漏\_ON\_线程\_终止参数


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
<td align="left">1</td>
<td align="left">该线程的地址</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">不释放条目的地址</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left"><p>指示项的状态的状态代码</p>
<p>0x1:锁指针不为 NULL</p>
<p>0x2:线程指针保留位已设置</p>
<p>0x3:线程指针已损坏</p>
<p>0x4:该条目有残留的 IO 或 CPU 提升左</p></td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">保留</td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

这通常被由于线程永远不会释放的锁之前获取 （例如，依赖于另一个线程释放它），或者如果线程没有提供一组一致的标志来锁定包 Api。

 

 




