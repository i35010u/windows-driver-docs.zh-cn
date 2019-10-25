---
title: WSK_TRANSPORT_LIST_QUERY
description: WSK_TRANSPORT_LIST_QUERY
ms.assetid: feb6aed2-fac9-4d3f-a36b-f721c737aacf
ms.date: 07/18/2017
keywords:
- WSK_TRANSPORT_LIST_QUERY 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 29817f14f61ee142e1f8a7ae249436a1d81e5f6e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844416"
---
# <a name="wsk_transport_list_query"></a>WSK\_传输\_列表\_查询


WSK 应用程序使用 WSK\_传输\_列表\_查询客户端控制操作来检索可在创建新套接字时指定的可用网络传输的列表。

若要检索可用网络传输的列表，WSK 应用程序需要使用以下参数调用[**WskControlClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client)函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>Value</th>
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
<td><p><strong>无效</strong></p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p><em>OutputBuffer</em>参数指向的结构数组的大小（以字节为单位）</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>指向接收可用网络传输列表的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_transport" data-raw-source="[&lt;strong&gt;WSK_TRANSPORT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_transport)"><strong>WSK_TRANSPORT</strong></a>结构的数组的指针</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>指向 SIZE_T 类型的变量的指针，该变量接收复制到由<em>OutputBuffer</em>参数指向的结构数组中的数据字节数。</p></td>
</tr>
<tr class="odd">
<td><p><em>Irp</em></p></td>
<td><p><strong>无效</strong></p></td>
</tr>
</tbody>
</table>

WSK 应用程序可以在*OutputSize*参数中指定零，并在*OutputBuffer*参数中指定**NULL** ，以确定[**WSK\_传输**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_transport)结构的数组大小（以字节为单位），该数组必须包含可用网络传输的完整列表。 在这种情况下，对[**WskControlClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client)函数的调用返回状态\_缓冲区\_溢出，并且*OutputSizeReturned*参数指向的变量包含所需的缓冲区大小。 然后，应用程序可以分配一个足够大的缓冲区来包含可用网络传输的完整列表，并可以第二次调用**WskControlClient**函数，并指定上表中显示的参数。

此客户端控制操作的*Irp*参数必须为**NULL** 。

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
<td>Wsk （包括 Wsk）</td>
</tr>
</tbody>
</table>

 

 




