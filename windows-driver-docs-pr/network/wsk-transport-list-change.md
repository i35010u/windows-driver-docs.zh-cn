---
title: WSK_TRANSPORT_LIST_CHANGE
description: WSK_TRANSPORT_LIST_CHANGE
ms.assetid: 3b12d692-467c-4d31-bd2a-bb6e34d87fde
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WSK_TRANSPORT_LIST_CHANGE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1f5a9e6657e6d1d4d58956ad99695e0da5370bb8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534690"
---
# <a name="wsktransportlistchange"></a>WSK\_传输\_列表\_更改


WSK 应用程序使用 WSK\_传输\_列表\_更改客户端管理操作，以接收通知，如果可用的网络的列表会传输更改。

若要接收通知的可用网络的列表时传输更改，WSK 应用程序调用[ **WskControlClient** ](https://msdn.microsoft.com/library/windows/hardware/ff571126)使用以下参数的函数。

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
<td><p>WSK_TRANSPORT_LIST_CHANGE</p></td>
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
<tr class="odd">
<td><p><em>Irp</em></p></td>
<td><p>指向由 WSK 子系统排队，直到可用的网络的列表会传输更改的 IRP 的指针。 WSK 子系统将完成 IRP 后添加新的网络传输或删除现有的网络传输。</p></td>
</tr>
</tbody>
</table>

IRP 是此客户端控制操作所必需的。

如果 WSK 应用程序调用 WSK 子系统将取消任何挂起的 Irp [ **WskDeregister** ](https://msdn.microsoft.com/library/windows/hardware/ff571128)从 WSK 子系统中分离本身。

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

 

 




