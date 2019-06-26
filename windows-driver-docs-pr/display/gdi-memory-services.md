---
title: GDI 内存服务
description: GDI 内存服务
ms.assetid: 60b45f8f-766b-498c-a0c2-3e93ea4b43b9
keywords:
- GDI WDK Windows 2000 显示，内存服务
- 图形驱动程序 WDK Windows 2000 显示，内存服务
- 绘制 WDK GDI，内存服务
- 内存 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75f76c761fe8bdfa2d4e776f9b1c7ebe453182ba
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354736"
---
# <a name="gdi-memory-services"></a>GDI 内存服务


## <span id="ddk_gdi_memory_services_gg"></span><span id="DDK_GDI_MEMORY_SERVICES_GG"></span>


GDI 到驱动程序编写人员，包括分配和释放系统内存、 用户内存、 专用的用户内存和视频内存的能力，以及锁定和解锁的内存范围的功能提供了一些与内存相关的服务。 下表列出了 GDI 内存服务。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engallocmem" data-raw-source="[&lt;strong&gt;EngAllocMem&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engallocmem)"><strong>EngAllocMem</strong></a></p></td>
<td align="left"><p>分配的内存块，并将插入之前分配的调用方提供的标记。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engallocprivateusermem" data-raw-source="[&lt;strong&gt;EngAllocPrivateUserMem&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engallocprivateusermem)"><strong>EngAllocPrivateUserMem</strong></a></p></td>
<td align="left"><p>从指定进程的地址空间分配的专用用户内存块，并将插入之前分配的调用方提供的标记。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engallocusermem" data-raw-source="[&lt;strong&gt;EngAllocUserMem&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engallocusermem)"><strong>EngAllocUserMem</strong></a></p></td>
<td align="left"><p>从当前进程的地址空间分配的内存块，并将插入之前分配的调用方提供的标记。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engfreemem" data-raw-source="[&lt;strong&gt;EngFreeMem&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engfreemem)"><strong>EngFreeMem</strong></a></p></td>
<td align="left"><p>释放系统内存分配的块<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engallocmem" data-raw-source="[&lt;strong&gt;EngAllocMem&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engallocmem)"> <strong>EngAllocMem</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engfreeprivateusermem" data-raw-source="[&lt;strong&gt;EngFreePrivateUserMem&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engfreeprivateusermem)"><strong>EngFreePrivateUserMem</strong></a></p></td>
<td align="left"><p>解除分配的专用用户分配的内存块<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engallocprivateusermem" data-raw-source="[&lt;strong&gt;EngAllocPrivateUserMem&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engallocprivateusermem)"> <strong>EngAllocPrivateUserMem</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engfreeusermem" data-raw-source="[&lt;strong&gt;EngFreeUserMem&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engfreeusermem)"><strong>EngFreeUserMem</strong></a></p></td>
<td align="left"><p>解除分配的用户分配的内存块<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engallocusermem" data-raw-source="[&lt;strong&gt;EngAllocUserMem&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engallocusermem)"> <strong>EngAllocUserMem</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsecuremem" data-raw-source="[&lt;strong&gt;EngSecureMem&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsecuremem)"><strong>EngSecureMem</strong></a></p></td>
<td align="left"><p>锁定在内存中指定的地址范围。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engunsecuremem" data-raw-source="[&lt;strong&gt;EngUnsecureMem&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engunsecuremem)"><strong>EngUnsecureMem</strong></a></p></td>
<td align="left"><p>解除锁定锁定的内存地址范围。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmemmgr/nf-dmemmgr-heapvidmemallocaligned" data-raw-source="[&lt;strong&gt;HeapVidMemAllocAligned&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmemmgr/nf-dmemmgr-heapvidmemallocaligned)"><strong>HeapVidMemAllocAligned</strong></a></p></td>
<td align="left"><p>分配<em>屏外内存</em>使用 DirectDraw 视频内存堆管理器的显示驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmemmgr/nf-dmemmgr-vidmemfree" data-raw-source="[&lt;strong&gt;VidMemFree&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmemmgr/nf-dmemmgr-vidmemfree)"><strong>VidMemFree</strong></a></p></td>
<td align="left"><p>释放由的显示驱动程序分配的屏幕外内存<a href="https://docs.microsoft.com/windows/desktop/api/dmemmgr/nf-dmemmgr-heapvidmemallocaligned" data-raw-source="[&lt;strong&gt;HeapVidMemAllocAligned&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmemmgr/nf-dmemmgr-heapvidmemallocaligned)"> <strong>HeapVidMemAllocAligned</strong></a>。</p></td>
</tr>
</tbody>
</table>

 

 

 





