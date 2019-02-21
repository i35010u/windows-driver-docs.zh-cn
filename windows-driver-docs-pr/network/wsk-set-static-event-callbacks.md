---
title: WSK_SET_STATIC_EVENT_CALLBACKS
description: WSK_SET_STATIC_EVENT_CALLBACKS
ms.assetid: fa95bc7d-c7b2-4cca-a419-ef5eb2520976
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WSK_SET_STATIC_EVENT_CALLBACKS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 19bee586264f06c08e2f8d8831d88ad743b4d2a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545005"
---
# <a name="wsksetstaticeventcallbacks"></a>WSK\_设置\_静态\_事件\_回调


WSK 应用程序使用 WSK\_设置\_静态\_事件\_回调客户端管理操作来自动启用它会创建每个套接字上的某些事件回调函数。 在这种方式中启用的事件回调函数始终处于启用状态，无法禁用或重新启用 WSK 应用程序的更高版本。 但是，如果 WSK 应用程序始终启用它会创建每个套接字上的某些事件回调函数，该应用程序应使用此方法来自动启用这些事件的回调函数，因为它将产生更好的性能。

如果 WSK 应用程序使用 WSK\_设置\_静态\_事件\_回调客户端管理操作，它必须执行此操作之前创建任何套接字。

若要自动启用它会创建每个套接字上的某些事件回调函数，WSK 应用程序调用[ **WskControlClient** ](https://msdn.microsoft.com/library/windows/hardware/ff571126)使用以下参数的函数。

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
<td><p><em>ControlCode</em></p></td>
<td><p>WSK_SET_STATIC_EVENT_CALLBACKS</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof(WSK_EVENT_CALLBACK_CONTROL)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>一个指向<a href="https://msdn.microsoft.com/library/windows/hardware/ff571166" data-raw-source="[&lt;strong&gt;WSK_EVENT_CALLBACK_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571166)"> <strong>WSK_EVENT_CALLBACK_CONTROL</strong> </a>结构，它指定所需的事件回调函数，来自动启用</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>Irp</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
</tbody>
</table>

WSK 应用程序可以指定不同的套接字类型中的事件标志的组合**EventMask**的成员[ **WSK\_事件\_回调\_控件** ](https://msdn.microsoft.com/library/windows/hardware/ff571166)结构。 WSK 子系统时 WSK 应用程序创建新的套接字，将自动启用特定于相应的事件回调函数[类别](https://msdn.microsoft.com/library/windows/hardware/ff571093)WSK 套接字正在创建。

有关标准 WSK 事件回调函数的事件标志的详细信息，请参阅[**因此\_WSK\_事件\_回调**](so-wsk-event-callback.md)。

有关启用和禁用套接字的事件回调函数的详细信息，请参阅[启用和禁用事件回调函数](https://msdn.microsoft.com/library/windows/hardware/ff548851)。

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
<td><p>版本</p></td>
<td><p>在 Windows Vista 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wsk.h （包括 Wsk.h）</td>
</tr>
</tbody>
</table>

 

 




