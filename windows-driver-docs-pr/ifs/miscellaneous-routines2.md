---
title: 杂项例程
description: 杂项例程
ms.assetid: e065c86c-a784-49e1-a1d9-e2bcff3fcae4
keywords:
- RDBSS WDK 的文件系统，其他例程
- 重定向驱动器缓冲子系统 WDK 的文件系统，其他例程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b0ec300244329940cbd655d9e7aa88ad8402908
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375963"
---
# <a name="miscellaneous-routines"></a>杂项例程


## <span id="ddk_miscellaneous_functions_if"></span><span id="DDK_MISCELLANEOUS_FUNCTIONS_IF"></span>


RDBSS 包括大量不属于特定类别的实用程序例程。

RDBSS 杂项例程包括：

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxfsddispatch" data-raw-source="[&lt;strong&gt;RxFsdDispatch&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxfsddispatch)"><strong>RxFsdDispatch</strong></a></p></td>
<td align="left"><p>此例程实现 RDBSS 来处理 I/O 请求数据包 (IRP) 文件系统驱动程序 (FSD) 调度。 此例程称为通过网络微型-重定向程序驱动程序调度例程启动 RDBSS 处理的请求中。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxfsdpostrequest" data-raw-source="[&lt;strong&gt;RxFsdPostRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxfsdpostrequest)"><strong>RxFsdPostRequest</strong></a></p></td>
<td align="left"><p>此例程排队 IRP 到辅助队列中等待处理的 RX_CONTEXT 结构由文件系统进程 (FSP)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxstruc/nf-rxstruc-rxgetrdbssprocess" data-raw-source="[&lt;strong&gt;RxGetRDBSSProcess&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxstruc/nf-rxstruc-rxgetrdbssprocess)"><strong>RxGetRDBSSProcess</strong></a></p></td>
<td align="left"><p>此例程返回一个指向 RDBSS 内核进程使用的主线程的过程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxisthisacscagentopen" data-raw-source="[&lt;strong&gt;RxIsThisACscAgentOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxisthisacscagentopen)"><strong>RxIsThisACscAgentOpen</strong></a></p></td>
<td align="left"><p>此例程确定是否一个文件打开请求已由用户模式下客户端的缓存代理。</p>
<p>此例程才可在 Windows Server 2003 上。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxmakelatedeviceavailable" data-raw-source="[&lt;strong&gt;RxMakeLateDeviceAvailable&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxmakelatedeviceavailable)"><strong>RxMakeLateDeviceAvailable</strong></a></p></td>
<td align="left"><p>此例程修改设备对象，从而使"后期设备"可用。 后期设备是指不在驱动程序的负载例程中创建。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxpreparetoreparsesymboliclink" data-raw-source="[&lt;strong&gt;RxPrepareToReparseSymbolicLink&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxpreparetoreparsesymboliclink)"><strong>RxPrepareToReparseSymbolicLink</strong></a></p></td>
<td align="left"><p>此例程设置文件的对象名称，以便重新分析。 网络微型-重定向程序使用此例程来遍历符号链接。 此例程不应通过网络微型-重定向程序。</p></td>
</tr>
</tbody>
</table>

 

 

 




