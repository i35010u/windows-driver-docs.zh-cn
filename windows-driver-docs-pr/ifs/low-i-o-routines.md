---
title: 低 I/O 例程
description: 低 I/O 例程
ms.assetid: 5317917d-9abc-43f9-ab4a-f070e491c816
keywords:
- RDBSS WDK 文件系统，低 i/o 例程
- 重定向驱动器缓冲子系统 WDK 文件系统、低 i/o 例程
- 低 i/o 例程 WDK RDBSS
- I/O WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36794726181c83baba0151e2dc1ebbd308a726c2
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067390"
---
# <a name="low-io-routines"></a>低 I/O 例程


## <span id="ddk_low_i_o_functions_if"></span><span id="DDK_LOW_I_O_FUNCTIONS_IF"></span>


低 i/o 例程表示对文件对象的基本 IRP \_ MJ \_ XXX 异步操作 (打开、关闭、读取和写入，例如) 。 RDBSS 提供了一些便利例程，可通过网络小型重定向器用于低 i/o 操作。 RDBSS 低 i/o 例程包括：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程所返回的值</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/lowio/nf-lowio-rxlowiocompletion" data-raw-source="[&lt;strong&gt;RxLowIoCompletion&lt;/strong&gt;](/windows-hardware/drivers/ddi/lowio/nf-lowio-rxlowiocompletion)"><strong>RxLowIoCompletion</strong></a></p></td>
<td align="left"><p>当处理完成时，如果最初以挂起状态返回例程，则必须由网络微型重定向程序驱动程序的低 i/o 例程调用此例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/lowio/nf-lowio-rxlowiogetbufferaddress" data-raw-source="[&lt;strong&gt;RxLowIoGetBufferAddress&lt;/strong&gt;](/windows-hardware/drivers/ddi/lowio/nf-lowio-rxlowiogetbufferaddress)"><strong>RxLowIoGetBufferAddress</strong></a></p></td>
<td align="left"><p>此例程返回与 RX_CONTEXT 结构的 <strong>LowIoContext</strong> 结构中的 MDL 相对应的缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxmapsystembuffer" data-raw-source="[&lt;strong&gt;RxMapSystemBuffer&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxmapsystembuffer)"><strong>RxMapSystemBuffer</strong></a></p></td>
<td align="left"><p>此例程返回 i/o 请求数据包 (IRP) 的系统缓冲区地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/rxnewmapuserbuffer" data-raw-source="[&lt;strong&gt;RxNewMapUserBuffer&lt;/strong&gt;](./rxnewmapuserbuffer.md)"><strong>RxNewMapUserBuffer</strong></a></p></td>
<td align="left"><p>此例程返回用于低 i/o 的用户缓冲区的地址。 请注意，此例程仅适用于 Windows XP 和 Windows 2000。</p></td>
</tr>
</tbody>
</table>

 

 

