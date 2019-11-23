---
title: WSK_TDI_BEHAVIOR
description: WSK_TDI_BEHAVIOR
ms.assetid: 84e4c8c3-2c31-4db5-bb25-309c6bb176ff
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WSK_TDI_BEHAVIOR 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3c18ae7179a59379c3e1e04a20682c392a67f438
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844424"
---
# <a name="wsk_tdi_behavior"></a>WSK\_TDI\_行为


**请注意**   TDI 功能已弃用，并将从 Microsoft Windows 的未来版本中删除。

 

WSK 应用程序使用 WSK\_TDI\_行为客户端控制操作控制 WSK 子系统是否会将网络 i/o 转移到[TDI](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565094(v=vs.85))传输。 仅当 WSK 应用程序需要替代 WSK 子系统的默认行为时，它才会使用此客户端控件操作。

如果 WSK 应用程序使用 WSK\_TDI\_行为客户端控制操作，则必须在创建任何套接字之前执行此操作。

为控制 WSK 子系统是否会将网络 i/o 转移到 TDI 传输，WSK 应用程序使用以下参数调用[**WskControlClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client)函数。

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
<td><p>WSK_TDI_BEHAVIOR</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof （ULONG）</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>指向 ULONG 类型化变量的指针，该变量包含控制 WSK 子系统的行为的标志。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p><strong>无效</strong></p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p><strong>无效</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>Irp</em></p></td>
<td><p><strong>无效</strong></p></td>
</tr>
</tbody>
</table>

为 WSK\_TDI\_行为客户端控制操作定义以下标志。

<a href="" id="wsk-tdi-behavior-bypass-tdi"></a>WSK\_TDI\_行为\_旁路\_TDI  
如果在 WSK 应用程序创建套接字时指定的地址族、套接字类型和协议存在本机 WSK 传输，则如果设置此标志，则 WSK 子系统将忽略任何 TDI 筛选器驱动程序并始终使用本机 WSK 传输。

默认行为是，如果检测到在 WSK 应用程序创建新的套接字时指定的地址族、套接字类型和协议的 TDI 筛选器驱动程序，WSK 子系统将新套接字到 TDI 传输的网络 i/o，以便网络流量和其他套接字操作通过 TDI 筛选器驱动程序。

此客户端控制操作的*Irp*参数必须为**NULL** 。

**请注意**，在 windows Vista 之后的 Microsoft Windows 版本中不支持  TDI。

 

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

 

 




