---
title: Winsock 内核调度表
description: Winsock 内核调度表
ms.assetid: 391c6868-fb85-41ea-ada5-6ba90750300c
keywords:
- 网络、 Winsock 内核 WDK 调度表
- WSK WDK 网络、 调度表
- 调度表 WDK Winsock 内核
- WDK Winsock 内核函数
- 基本套接字 WDK Winsock 内核
- 侦听套接字 WDK Winsock 内核
- 数据报套接字 WDK Winsock 内核
- 面向连接的套接字 WDK Winsock 内核
- 事件回调函数 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c62de8e85bfd1ca9251bf5ae7a6c19e0d9eb8d41
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548048"
---
# <a name="winsock-kernel-dispatch-tables"></a>Winsock 内核调度表


[套接字对象](winsock-kernel-objects.md)的 Winsock Kernel (WSK) 套接字包含提供程序调度表结构，其中包含指向支持的套接字的套接字函数的函数指针的指针。 WSK 应用程序提供程序调度表结构，以执行套接字的网络 I/O 操作中调用函数。 因为每个 WSK[套接字类别](winsock-kernel-socket-categories.md)支持一组不同的套接字函数，WSK[网络编程接口 (NPI)](network-programming-interface.md)定义的每个类别的不同的提供程序调度表结构WSK 套接字。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">套接字类别</th>
<th align="left">调度表结构</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>基本的套接字</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff571171" data-raw-source="[&lt;strong&gt;WSK_PROVIDER_BASIC_DISPATCH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571171)"><strong>WSK_PROVIDER_BASIC_DISPATCH</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>侦听套接字</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff571176" data-raw-source="[&lt;strong&gt;WSK_PROVIDER_LISTEN_DISPATCH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571176)"><strong>WSK_PROVIDER_LISTEN_DISPATCH</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>数据报套接字</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff571174" data-raw-source="[&lt;strong&gt;WSK_PROVIDER_DATAGRAM_DISPATCH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571174)"><strong>WSK_PROVIDER_DATAGRAM_DISPATCH</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>面向连接的套接字</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff571173" data-raw-source="[&lt;strong&gt;WSK_PROVIDER_CONNECTION_DISPATCH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571173)"><strong>WSK_PROVIDER_CONNECTION_DISPATCH</strong></a></p></td>
</tr>
</tbody>
</table>

 

如果 WSK 应用程序使用它创建的套接字事件回调函数，它必须提供客户端调度表结构，其中包含指向套接字的事件回调函数的函数，每当创建新的套接字时。 由于每个 WSK 套接字类别支持一组不同的事件回调函数，因此 WSK NPI 定义 WSK 套接字的每个类别的不同的客户端调度表结构。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">套接字类别</th>
<th align="left">调度表结构</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>侦听套接字</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff571162" data-raw-source="[&lt;strong&gt;WSK_CLIENT_LISTEN_DISPATCH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571162)"><strong>WSK_CLIENT_LISTEN_DISPATCH</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>数据报套接字</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff571158" data-raw-source="[&lt;strong&gt;WSK_CLIENT_DATAGRAM_DISPATCH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571158)"><strong>WSK_CLIENT_DATAGRAM_DISPATCH</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>面向连接的套接字</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff571156" data-raw-source="[&lt;strong&gt;WSK_CLIENT_CONNECTION_DISPATCH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571156)"><strong>WSK_CLIENT_CONNECTION_DISPATCH</strong></a></p></td>
</tr>
</tbody>
</table>

 

**请注意**  基本套接字不支持任何事件回调函数。 因此，任何客户端调度表结构不定义基本的套接字。

 

 

 





