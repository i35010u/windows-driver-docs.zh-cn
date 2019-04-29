---
title: 低 I/O 例程
description: 低 I/O 例程
ms.assetid: 5317917d-9abc-43f9-ab4a-f070e491c816
keywords:
- RDBSS WDK 的文件系统，低 I/O 例程
- 重定向驱动器缓冲子系统 WDK 的文件系统，低 I/O 例程
- 较低的 I/O 例程 WDK RDBSS
- I/O WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79cc867bfa40ec251c06282269b7cdd61394fae6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324371"
---
# <a name="low-io-routines"></a>低 I/O 例程


## <span id="ddk_low_i_o_functions_if"></span><span id="DDK_LOW_I_O_FUNCTIONS_IF"></span>


低 I/O 例程表示基本 IRP\_MJ\_XXX 上的文件对象的异步操作 （打开、 关闭读取，并编写，例如）。 RDBSS 提供较低的 I/O 操作由网络微型重定向某些方便例程。 RDBSS 低 I/O 例程包括：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554525" data-raw-source="[&lt;strong&gt;RxLowIoCompletion&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554525)"><strong>RxLowIoCompletion</strong></a></p></td>
<td align="left"><p>此例程必须调用由网络微型重定向程序驱动程序的较低的 I/O 例程处理完成后，如果该例程返回的最初为挂起。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554529" data-raw-source="[&lt;strong&gt;RxLowIoGetBufferAddress&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554529)"><strong>RxLowIoGetBufferAddress</strong></a></p></td>
<td align="left"><p>此例程返回对应的缓冲区到从 MDL <strong>LowIoContext</strong> RX_CONTEXT 结构的结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554549" data-raw-source="[&lt;strong&gt;RxMapSystemBuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554549)"><strong>RxMapSystemBuffer</strong></a></p></td>
<td align="left"><p>此例程返回 I/O 请求数据包 (IRP) 从系统缓冲区地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554591" data-raw-source="[&lt;strong&gt;RxNewMapUserBuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554591)"><strong>RxNewMapUserBuffer</strong></a></p></td>
<td align="left"><p>此例程将返回为低 I/O 所使用的用户缓冲区的地址。 请注意，此例程仅可在 Windows XP 和 Windows 2000 上。</p></td>
</tr>
</tbody>
</table>

 

 

 




