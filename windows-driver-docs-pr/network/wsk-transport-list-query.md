---
title: WSK_TRANSPORT_LIST_QUERY
description: WSK_TRANSPORT_LIST_QUERY
ms.assetid: feb6aed2-fac9-4d3f-a36b-f721c737aacf
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WSK_TRANSPORT_LIST_QUERY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1d3db89c4885f1dfec1c5b43fdb1e233f229584d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379705"
---
# <a name="wsktransportlistquery"></a>WSK\_传输\_列表\_查询


WSK 应用程序使用 WSK\_传输\_列表\_查询客户端管理操作来检索可在创建新的套接字时指定的可用的网络传输的列表。

若要检索一系列可用的网络传输，WSK 应用程序调用[ **WskControlClient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_client)使用以下参数的函数。

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
<td><p><em>ControlCode</em></p></td>
<td><p>WSK_TRANSPORT_LIST_QUERY</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>大小 （字节） 所指向的结构数组<em>OutputBuffer</em>参数</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>指向数组的指针<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_transport" data-raw-source="[&lt;strong&gt;WSK_TRANSPORT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_transport)"> <strong>WSK_TRANSPORT</strong> </a>接收可用的网络传输的列表的结构</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>指向一个 SIZE_T 类型的变量来接收的数据复制到所指向的结构数组的字节数的指针<em>OutputBuffer</em>参数</p></td>
</tr>
<tr class="odd">
<td><p><em>Irp</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
</tbody>
</table>

WSK 应用程序可以指定在零*OutputSize*参数和**NULL**中*OutputBuffer*参数，以确定的数组的大小[ **WSK\_传输**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_transport)结构，以字节为单位，需包含可用的网络传输的完整列表。 在这种情况下，调用[ **WskControlClient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_client)函数将返回状态\_缓冲区\_溢出和所指向的变量*OutputSizeReturned*参数包含所需的缓冲区大小。 然后，应用程序可分配的缓冲区的大小足以包含可用的网络传输的完整列表，可以调用**WskControlClient**函数指定的参数中所示的第二次上表中。

*Irp*参数必须是**NULL**此客户端控制操作。

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

 

 




