---
title: WSK_TDI_BEHAVIOR
description: WSK_TDI_BEHAVIOR
ms.assetid: 84e4c8c3-2c31-4db5-bb25-309c6bb176ff
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WSK_TDI_BEHAVIOR 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6321bd798bdec847caaefa8a4dddc517cf5e645a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567940"
---
# <a name="wsktdibehavior"></a>WSK\_TDI\_BEHAVIOR


**请注意**   TDI 功能已弃用，将 Microsoft Windows 的未来版本中删除。

 

WSK 应用程序使用 WSK\_TDI\_行为客户端控制来控制操作是否 WSK 子系统将转移到的网络 I/O [TDI](https://msdn.microsoft.com/library/windows/hardware/ff565094)传输。 WSK 应用程序使用此客户端管理操作，仅当其需要重写 WSK 子系统的默认行为。

如果 WSK 应用程序使用 WSK\_TDI\_行为客户端管理操作，它必须执行此操作之前创建任何套接字。

若要控制是否 WSK 子系统将转移到 TDI 传输的网络 I/O，WSK 应用程序调用[ **WskControlClient** ](https://msdn.microsoft.com/library/windows/hardware/ff571126)使用以下参数的函数。

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
<td><p>WSK_TDI_BEHAVIOR</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof(ULONG)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>指向 ULONG 的指针类型化变量，其中包含控制 WSK 子系统的行为的标志。</p></td>
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

以下标志定义用于 WSK\_TDI\_行为客户端管理操作。

<a href="" id="wsk-tdi-behavior-bypass-tdi"></a>WSK\_TDI\_BEHAVIOR\_BYPASS\_TDI  
如果本机 WSK 传输存在地址族、 套接字类型和 WSK 应用程序创建的套接字时所指定的协议，然后，如果设置此标志，WSK 子系统将忽略任何 TDI 筛选器驱动程序并始终使用本机 WSK 传输。

默认行为是，如果 TDI 筛选器驱动程序检测到的地址族、 套接字类型和 WSK 应用程序创建一个新的套接字时所指定的协议，WSK 子系统会将网络 I/O 的新套接字 TDI 传输到这样的网络流量和其他套接字操作通过 TDI 筛选器驱动程序。

*Irp*参数必须是**NULL**此客户端控制操作。

**请注意**  TDI 之后，不再支持 Microsoft Windows 版本中 Windows Vista。

 

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
<td><p>Header</p></td>
<td>Wsk.h （包括 Wsk.h）</td>
</tr>
</tbody>
</table>

 

 




