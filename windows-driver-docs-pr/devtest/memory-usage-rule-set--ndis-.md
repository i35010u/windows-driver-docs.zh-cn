---
title: 内存用法规则集 (NDIS)
description: 使用这些规则验证驱动程序是否正确调用 NDIS 函数以分配和释放内存。
ms.assetid: F28314C6-4B4D-479F-BB96-6850C8F98153
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: efc74cda3cfa0984c530a55e1c371199202d420c
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103394"
---
# <a name="memory-usage-rule-set-ndis"></a>内存用法规则集 (NDIS)


使用这些规则验证驱动程序是否正确调用 NDIS 函数以分配和释放内存。

## <a name="in-this-section"></a>在本节中


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="ndis-ndisallocategenericobject.md" data-raw-source="[&lt;strong&gt;NdisAllocateGenericObject&lt;/strong&gt;](ndis-ndisallocategenericobject.md)"><strong>NdisAllocateGenericObject</strong></a></p></td>
<td align="left"><p><a href="ndis-ndisallocategenericobject.md" data-raw-source="[&lt;strong&gt;NdisAllocateGenericObject&lt;/strong&gt;](ndis-ndisallocategenericobject.md)"><strong>NdisAllocateGenericObject</strong></a>规则指定按替代顺序调用<a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocategenericobject" data-raw-source="[&lt;strong&gt;NdisAllocateGenericObject&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocategenericobject)"><strong>NdisAllocateGenericObject</strong></a>和<a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreegenericobject" data-raw-source="[&lt;strong&gt;NdisFreeGenericObject&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreegenericobject)"><strong>NdisFreeGenericObject</strong></a> 。 最终的目标是确保在 <a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)"><em>MiniportHaltEx</em></a> 结束时释放所有泛型对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndisallocatemdl.md" data-raw-source="[&lt;strong&gt;NdisAllocateMdl&lt;/strong&gt;](ndis-ndisallocatemdl.md)"><strong>NdisAllocateMdl</strong></a></p></td>
<td align="left"><p><a href="ndis-ndisallocatemdl.md" data-raw-source="[&lt;strong&gt;NdisAllocateMdl&lt;/strong&gt;](ndis-ndisallocatemdl.md)"><strong>NdisAllocateMdl</strong></a>规则指定按替代顺序调用<a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatemdl" data-raw-source="[&lt;strong&gt;NdisAllocateMdl&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatemdl)"><strong>NdisAllocateMdl</strong></a>和<a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreemdl" data-raw-source="[&lt;strong&gt;NdisFreeMdl&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreemdl)"><strong>NdisFreeMdl</strong></a> 。 最终目标是确保在 <a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)"><em>MiniportHaltEx</em></a> 结束时释放所有 MDLs。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndisallocatememorywithtagpriority.md" data-raw-source="[&lt;strong&gt;NdisAllocateMemoryWithTagPriority&lt;/strong&gt;](ndis-ndisallocatememorywithtagpriority.md)"><strong>NdisAllocateMemoryWithTagPriority</strong></a></p></td>
<td align="left"><p><a href="ndis-ndisallocatememorywithtagpriority.md" data-raw-source="[&lt;strong&gt;NdisAllocateMemoryWithTagPriority&lt;/strong&gt;](ndis-ndisallocatememorywithtagpriority.md)"><strong>NdisAllocateMemoryWithTagPriority</strong></a>规则指定驱动程序不得在不提供<em>标记</em>的情况下调用<strong>NdisAllocateMemoryWithTagPriority</strong> 。</p>
<p>每个内存分配应使用唯一的池标记，以确保内核调试器和驱动程序验证器可以识别不同的已分配内存块。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndisallocatenetbuffer.md" data-raw-source="[&lt;strong&gt;NdisAllocateNetBuffer&lt;/strong&gt;](ndis-ndisallocatenetbuffer.md)"><strong>NdisAllocateNetBuffer</strong></a></p></td>
<td align="left"><p><a href="ndis-ndisallocatenetbuffer.md" data-raw-source="[&lt;strong&gt;NdisAllocateNetBuffer&lt;/strong&gt;](ndis-ndisallocatenetbuffer.md)"><strong>NdisAllocateNetBuffer</strong></a>规则指定按替代顺序调用<a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbuffer" data-raw-source="[&lt;strong&gt;NdisAllocateNetBuffer&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbuffer)"><strong>NdisAllocateNetBuffer</strong></a>和<a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbuffer" data-raw-source="[&lt;strong&gt;NdisFreeNetBuffer&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbuffer)"><strong>NdisFreeNetBuffer</strong></a> 。 最终的目标是确保在<a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)"><em>MiniportHaltEx</em></a>结束时释放<a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer" data-raw-source="[&lt;strong&gt;NET_BUFFER&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)"><strong>NET_BUFFER</strong></a>的所有实例。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndismfreesharedmemory.md" data-raw-source="[&lt;strong&gt;NdisMFreeSharedMemory&lt;/strong&gt;](ndis-ndismfreesharedmemory.md)"><strong>NdisMFreeSharedMemory</strong></a></p></td>
<td align="left"><p>不能从<a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown" data-raw-source="[&lt;em&gt;MiniportShutdownEx&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown)"><em>MiniportShutdownEx</em></a>函数调用<a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreesharedmemory" data-raw-source="[&lt;strong&gt;NdisMFreeSharedMemory&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreesharedmemory)"><strong>NdisMFreeSharedMemory</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndismindicatestatusex.md" data-raw-source="[&lt;strong&gt;NdisMIndicateStatusEx&lt;/strong&gt;](ndis-ndismindicatestatusex.md)"><strong>NdisMIndicateStatusEx</strong></a></p></td>
<td align="left"><p>驱动程序从<a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)"><em>MiniportHaltEx</em></a>函数返回后，不能调用<a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex" data-raw-source="[&lt;strong&gt;NdisMIndicateStatusEx&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)"><strong>NdisMIndicateStatusEx</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndismmapiospace.md" data-raw-source="[&lt;strong&gt;NdisMMapIoSpace&lt;/strong&gt;](ndis-ndismmapiospace.md)"><strong>NdisMMapIoSpace</strong></a></p></td>
<td align="left"><p>只应在<a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize" data-raw-source="[&lt;em&gt;MiniportInitializeEx&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)"><em>MiniportInitializeEx</em></a>的上下文中调用<a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismmapiospace" data-raw-source="[&lt;strong&gt;NdisMMapIoSpace&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismmapiospace)"><strong>NdisMMapIoSpace</strong></a>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndismregisterioportrange.md" data-raw-source="[&lt;strong&gt;NdisMRegisterIoPortRange&lt;/strong&gt;](ndis-ndismregisterioportrange.md)"><strong>NdisMRegisterIoPortRange</strong></a></p></td>
<td align="left"><p>微型端口驱动程序从其<a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize" data-raw-source="[&lt;em&gt;MiniportInitializeEx&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)"><em>MiniportInitializeEx</em></a>或 MINIPORT_ADD_DEVICE 函数调用<a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterioportrange" data-raw-source="[&lt;strong&gt;NdisMRegisterIoPortRange&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterioportrange)"><strong>NdisMRegisterIoPortRange</strong></a> 。 <em>MiniportInitializeEx</em> 或 MINIPORT_ADD_DEVICE 必须先调用 <a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes" data-raw-source="[&lt;strong&gt;NdisMSetMiniportAttributes&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)"><strong>NdisMSetMiniportAttributes</strong></a> ，然后才能调用 <strong>NdisMRegisterIoPortRange</strong>。</p></td>
</tr>
</tbody>
</table>

 

**选择内存使用规则集**

1.  选择你的驱动程序项目 () 在 Microsoft Visual Studio 中。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

2.  单击 " **规则** " 选项卡。在 " **规则集**" 下，选择 **MemoryUsage**。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请使用 **/check**选项指定**MemoryUsage。 sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:MemoryUsage.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md) 和 [静态驱动程序验证程序命令 (MSBuild) ](./-static-driver-verifier-commands--msbuild-.md)。

