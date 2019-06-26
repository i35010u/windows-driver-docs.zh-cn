---
title: 内存用法规则集 (NDIS)
description: 使用这些规则来验证您的驱动程序正确调用 NDIS 函数来分配和释放内存。
ms.assetid: F28314C6-4B4D-479F-BB96-6850C8F98153
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: e9de9dadaf10539fda1b9774d6b9c078814e0b01
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354765"
---
# <a name="memory-usage-rule-set-ndis"></a>内存用法规则集 (NDIS)


使用这些规则来验证您的驱动程序正确调用 NDIS 函数来分配和释放内存。

## <a name="in-this-section"></a>本节内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="ndis-ndisallocategenericobject.md" data-raw-source="[&lt;strong&gt;NdisAllocateGenericObject&lt;/strong&gt;](ndis-ndisallocategenericobject.md)"><strong>NdisAllocateGenericObject</strong></a></p></td>
<td align="left"><p><a href="ndis-ndisallocategenericobject.md" data-raw-source="[&lt;strong&gt;NdisAllocateGenericObject&lt;/strong&gt;](ndis-ndisallocategenericobject.md)"> <strong>NdisAllocateGenericObject</strong> </a>规则指定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocategenericobject" data-raw-source="[&lt;strong&gt;NdisAllocateGenericObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocategenericobject)"> <strong>NdisAllocateGenericObject</strong> </a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreegenericobject" data-raw-source="[&lt;strong&gt;NdisFreeGenericObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreegenericobject)"> <strong>NdisFreeGenericObject</strong> </a>备用顺序调用。 最终目标是确保所有泛型对象也将释放时<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)"> <em>MiniportHaltEx</em> </a>结束。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndisallocatemdl.md" data-raw-source="[&lt;strong&gt;NdisAllocateMdl&lt;/strong&gt;](ndis-ndisallocatemdl.md)"><strong>NdisAllocateMdl</strong></a></p></td>
<td align="left"><p><a href="ndis-ndisallocatemdl.md" data-raw-source="[&lt;strong&gt;NdisAllocateMdl&lt;/strong&gt;](ndis-ndisallocatemdl.md)"> <strong>NdisAllocateMdl</strong> </a>规则指定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatemdl" data-raw-source="[&lt;strong&gt;NdisAllocateMdl&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatemdl)"> <strong>NdisAllocateMdl</strong> </a>并<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreemdl" data-raw-source="[&lt;strong&gt;NdisFreeMdl&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreemdl)"> <strong>NdisFreeMdl</strong></a>备用顺序调用。 最终目标是确保所有 MDLs 时释放<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)"> <em>MiniportHaltEx</em> </a>结束。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndisallocatememorywithtagpriority.md" data-raw-source="[&lt;strong&gt;NdisAllocateMemoryWithTagPriority&lt;/strong&gt;](ndis-ndisallocatememorywithtagpriority.md)"><strong>NdisAllocateMemoryWithTagPriority</strong></a></p></td>
<td align="left"><p><a href="ndis-ndisallocatememorywithtagpriority.md" data-raw-source="[&lt;strong&gt;NdisAllocateMemoryWithTagPriority&lt;/strong&gt;](ndis-ndisallocatememorywithtagpriority.md)"> <strong>NdisAllocateMemoryWithTagPriority</strong> </a>规则指定一个驱动程序必须调用<strong>NdisAllocateMemoryWithTagPriority</strong>而无需提供<em>标记</em>。</p>
<p>每个内存分配应使用唯一池标记来确保内核调试程序和驱动程序验证程序可以标识不同分配的内存块。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndisallocatenetbuffer.md" data-raw-source="[&lt;strong&gt;NdisAllocateNetBuffer&lt;/strong&gt;](ndis-ndisallocatenetbuffer.md)"><strong>NdisAllocateNetBuffer</strong></a></p></td>
<td align="left"><p><a href="ndis-ndisallocatenetbuffer.md" data-raw-source="[&lt;strong&gt;NdisAllocateNetBuffer&lt;/strong&gt;](ndis-ndisallocatenetbuffer.md)"> <strong>NdisAllocateNetBuffer</strong> </a>规则指定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatenetbuffer" data-raw-source="[&lt;strong&gt;NdisAllocateNetBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatenetbuffer)"> <strong>NdisAllocateNetBuffer</strong> </a>并<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreenetbuffer" data-raw-source="[&lt;strong&gt;NdisFreeNetBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreenetbuffer)"> <strong>NdisFreeNetBuffer</strong> </a>备用顺序调用。 最终目标是确保所有实例的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer" data-raw-source="[&lt;strong&gt;NET_BUFFER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)"> <strong>NET_BUFFER</strong> </a>时释放<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)"> <em>MiniportHaltEx</em> </a>结束。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndismfreesharedmemory.md" data-raw-source="[&lt;strong&gt;NdisMFreeSharedMemory&lt;/strong&gt;](ndis-ndismfreesharedmemory.md)"><strong>NdisMFreeSharedMemory</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismfreesharedmemory" data-raw-source="[&lt;strong&gt;NdisMFreeSharedMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismfreesharedmemory)"><strong>NdisMFreeSharedMemory</strong> </a>不能从调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_shutdown" data-raw-source="[&lt;em&gt;MiniportShutdownEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_shutdown)"> <em>MiniportShutdownEx</em> </a>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndismindicatestatusex.md" data-raw-source="[&lt;strong&gt;NdisMIndicateStatusEx&lt;/strong&gt;](ndis-ndismindicatestatusex.md)"><strong>NdisMIndicateStatusEx</strong></a></p></td>
<td align="left"><p>该驱动程序不能调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex" data-raw-source="[&lt;strong&gt;NdisMIndicateStatusEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)"> <strong>NdisMIndicateStatusEx</strong> </a>它将返回后<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)"> <em>MiniportHaltEx</em> </a>函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndismmapiospace.md" data-raw-source="[&lt;strong&gt;NdisMMapIoSpace&lt;/strong&gt;](ndis-ndismmapiospace.md)"><strong>NdisMMapIoSpace</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismmapiospace" data-raw-source="[&lt;strong&gt;NdisMMapIoSpace&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismmapiospace)"> <strong>NdisMMapIoSpace</strong> </a>函数只应调用的上下文中<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize" data-raw-source="[&lt;em&gt;MiniportInitializeEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)"> <em>MiniportInitializeEx</em></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndismregisterioportrange.md" data-raw-source="[&lt;strong&gt;NdisMRegisterIoPortRange&lt;/strong&gt;](ndis-ndismregisterioportrange.md)"><strong>NdisMRegisterIoPortRange</strong></a></p></td>
<td align="left"><p>微型端口驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterioportrange" data-raw-source="[&lt;strong&gt;NdisMRegisterIoPortRange&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterioportrange)"> <strong>NdisMRegisterIoPortRange</strong> </a>从其<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize" data-raw-source="[&lt;em&gt;MiniportInitializeEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)"> <em>MiniportInitializeEx</em> </a>或 MINIPORT_ADD_DEVICE 函数。 <em>MiniportInitializeEx</em>也必须调用 MINIPORT_ADD_DEVICE <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes" data-raw-source="[&lt;strong&gt;NdisMSetMiniportAttributes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)"> <strong>NdisMSetMiniportAttributes</strong> </a>之前，调用<strong>NdisMRegisterIoPortRange</strong>。</p></td>
</tr>
</tbody>
</table>

 

**若要选择内存使用率规则设置**

1.  Microsoft Visual Studio 中选择您的驱动程序项目 (.vcxProj)。 从**驱动程序**菜单上，单击**启动 Static Driver Verifier...** .

2.  单击**规则**选项卡。下**规则集**，选择**MemoryUsage**。

    若要选择的默认规则集从 Visual Studio 开发人员命令提示符窗口，请指定**MemoryUsage.sdv**与 **/check**选项。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:MemoryUsage.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅[以找到缺陷驱动程序中使用 Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)并[Static Driver Verifier 命令 (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)。

 

 





