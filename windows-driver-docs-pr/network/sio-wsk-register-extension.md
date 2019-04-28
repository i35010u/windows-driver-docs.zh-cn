---
title: SIO_WSK_REGISTER_EXTENSION
description: SIO_WSK_REGISTER_EXTENSION
ms.assetid: e7fd6d68-85e8-4c5f-b67f-2193d200130d
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 SIO_WSK_REGISTER_EXTENSION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 722f69616475e59f1a343f5895a9afd513b5fefd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351677"
---
# <a name="siowskregisterextension"></a>SIO\_WSK\_注册\_扩展


SIO\_WSK\_注册\_扩展套接字 I/O 控制操作允许 WSK 的应用程序注册受 WSK 子系统的扩展接口。 此套接字的 I/O 控制操作适用于所有套接字类型。

若要注册的扩展接口，WSK 应用程序调用[ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)使用以下参数的函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskIoctl</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SIO_WSK_REGISTER_EXTENSION</p></td>
</tr>
<tr class="odd">
<td><p><em>Level</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof(WSK_EXTENSION_CONTROL_IN)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>一个指向<a href="https://msdn.microsoft.com/library/windows/hardware/ff571167" data-raw-source="[&lt;strong&gt;WSK_EXTENSION_CONTROL_IN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571167)"> <strong>WSK_EXTENSION_CONTROL_IN</strong> </a>结构。 此结构包含一个指向<a href="https://msdn.microsoft.com/library/windows/hardware/ff568373" data-raw-source="[Network Programming Interface (NPI)](https://msdn.microsoft.com/library/windows/hardware/ff568373)">网络编程接口 (NPI)</a>标识符的扩展插件接口和调度表和 WSK 应用程序的扩展插件实现的上下文的指针接口。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>sizeof(WSK_EXTENSION_CONTROL_OUT)</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>一个指向<a href="https://msdn.microsoft.com/library/windows/hardware/ff571168" data-raw-source="[&lt;strong&gt;WSK_EXTENSION_CONTROL_OUT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571168)"> <strong>WSK_EXTENSION_CONTROL_OUT</strong> </a>结构。 此结构接收一个指向调度表和 WSK 子系统的扩展接口实现的上下文的指针。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>


WSK 应用程序调用时未指定指向 IRP **WskControlSocket**函数以注册一个扩展接口。

调度表结构的内容是特定于接口的扩展。

有关注册的扩展接口的详细信息，请参阅[注册一个扩展接口](https://msdn.microsoft.com/library/windows/hardware/ff570461)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>在 Windows Vista 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wsk.h （包括 Wsk.h）</td>
</tr>
</tbody>
</table>

 

 




