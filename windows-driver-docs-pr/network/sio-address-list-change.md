---
title: SIO_ADDRESS_LIST_CHANGE
description: SIO_ADDRESS_LIST_CHANGE
ms.assetid: d451208d-c850-4f2f-9ee0-d34139454ed4
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 SIO_ADDRESS_LIST_CHANGE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bfb3f9f96087e2cf76f0df1ff01fc8db178f0d81
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524935"
---
# <a name="sioaddresslistchange"></a>SIO\_地址\_列表\_更改


SIO\_地址\_列表\_更改套接字 I/O 控制操作通知 WSK 应用程序时对套接字地址族的本地传输地址的列表的更改。 此套接字的 I/O 控制操作适用于所有套接字类型。

已对套接字地址族的本地传输地址的列表的更改时收到通知，WSK 应用程序调用[ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)使用以下参数的函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskIoctl</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SIO_ADDRESS_LIST_CHANGE</p></td>
</tr>
<tr class="odd">
<td><p><em>Level</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>

WSK 应用程序调用时必须指定一个指向 IRP **WskControlSocket**函数的套接字地址族的本地传输地址的列表的更改通知。 WSK 子系统排队 IRP，并返回状态\_PENDING。 如果更改的套接字地址族的本地传输地址的列表，WSK 子系统完成 IRP。 WSK 应用程序调用 IRP 的完成例程时，可以使用[ **SIO\_地址\_列表\_查询**](sio-address-list-query.md)套接字来查询新的 I/O 控制操作套接字的地址族的本地传输地址的列表。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 Windows Vista 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ws2def.h （包括 Wsk.h）</td>
</tr>
</tbody>
</table>

 

 




