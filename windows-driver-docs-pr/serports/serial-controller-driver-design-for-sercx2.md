---
title: SerCx2 串行控制器驱动程序设计
description: 若要管理串行控制器，你编写执行特定于硬件的任务，并与 SerCx2 进行通信的串行控制器驱动程序。
ms.assetid: 67045E19-4EE1-4C31-A842-858E9A90233E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a40c31e5d9c016d02477efb2541854cbd6af487c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534488"
---
# <a name="serial-controller-driver-design-for-sercx2"></a>SerCx2 串行控制器驱动程序设计


若要管理串行控制器，你编写执行特定于硬件的任务，并与 SerCx2 进行通信的串行控制器驱动程序。 从 Windows 8.1 开始，SerCx2 是系统提供的组件，它处理许多通用串行控制器的这些处理任务。 这些任务包括管理超时值以及处理读取和写入串行控制器的客户端发送的请求。

## <a name="in-this-section"></a>本部分内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="features-of-sercx2-based-serial-controller-drivers.md" data-raw-source="[Features of SerCx2-Based Serial Controller Drivers](features-of-sercx2-based-serial-controller-drivers.md)">SerCx2 基于串行控制器驱动程序的功能</a></p></td>
<td><p>SerCx2 基于串行控制器驱动程序是 KMDF 驱动程序的使用方法和回调中的 KMDF 执行通用驱动程序操作，并与 SerCx2 来执行特定于串行控制器驱动程序的操作的通信。</p></td>
</tr>
<tr class="even">
<td><p><a href="sercx2-i-o-transactions.md" data-raw-source="[SerCx2 I/O Transactions](sercx2-i-o-transactions.md)">SerCx2 I/O 事务</a></p></td>
<td><p>SerCx2 简化了读取的处理 (<a href="https://msdn.microsoft.com/library/windows/hardware/ff546883" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546883)"><strong>IRP_MJ_READ</strong></a>) 和写入 (<a href="https://msdn.microsoft.com/library/windows/hardware/ff546904" data-raw-source="[&lt;strong&gt;IRP_MJ_WRITE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546904)"><strong>IRP_MJ_WRITE</strong></a>) 适用于你串行控制器的请求驱动程序。 读取或写入请求的响应，SerCx2 向串行控制器驱动程序发出一个或多个 I/O 事务。 该驱动程序从&#39;s 角度来看，每个事务是一种简单和完成 I/O 操作。</p></td>
</tr>
</tbody>
</table>

 

 

 




