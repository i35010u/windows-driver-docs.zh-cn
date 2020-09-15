---
title: DDI 用法规则集 (NDIS)
description: 使用这些规则验证驱动程序正确使用 NDIS DDIs。
ms.assetid: A109A452-D3A7-4204-B267-1F0F98652597
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8dae3069597a66f50bf67dd16e9771c314436bfd
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103112"
---
# <a name="ddi-usage-rule-set-ndis"></a>DDI 用法规则集 (NDIS)


使用这些规则验证驱动程序正确使用 NDIS DDIs。

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
<td align="left"><p><a href="ndis-init-deregisterinterrupt.md" data-raw-source="[&lt;strong&gt;Init_DeRegisterInterrupt&lt;/strong&gt;](ndis-init-deregisterinterrupt.md)"><strong>Init_DeRegisterInterrupt</strong></a></p></td>
<td align="left"><p><a href="ndis-init-deregisterinterrupt.md" data-raw-source="[&lt;strong&gt;Init_DeRegisterInterrupt&lt;/strong&gt;](ndis-init-deregisterinterrupt.md)"><strong>Init_DeRegisterInterrupt</strong></a>规则指定在 MPInitilize 期间至少调用一次<a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterinterruptex" data-raw-source="[&lt;strong&gt;NdisMRegisterInterruptEx&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterinterruptex)"><strong>NdisMRegisterInterruptEx</strong></a> ，在 MPHaltEx 中至少应调用一次<a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterinterruptex" data-raw-source="[&lt;strong&gt;NdisMDeregisterInterruptEx&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterinterruptex)"><strong>NdisMDeregisterInterruptEx</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-init-ndisallocateioworkitem.md" data-raw-source="[&lt;strong&gt;Init_NdisAllocateIoWorkItem&lt;/strong&gt;](ndis-init-ndisallocateioworkitem.md)"><strong>Init_NdisAllocateIoWorkItem</strong></a></p></td>
<td align="left"><p><a href="ndis-init-ndisallocateioworkitem.md" data-raw-source="[&lt;strong&gt;Init_NdisAllocateIoWorkItem&lt;/strong&gt;](ndis-init-ndisallocateioworkitem.md)"><strong>Init_NdisAllocateIoWorkItem</strong></a>规则指定在<a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize" data-raw-source="[&lt;em&gt;MiniportInitializeEx&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)"><em>MiniportInitializeEx</em></a>期间，如果至少调用了<a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocateioworkitem" data-raw-source="[&lt;strong&gt;NdisAllocateIoWorkItem&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocateioworkitem)"><strong>NdisAllocateIoWorkItem</strong></a> ，则<a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreeioworkitem" data-raw-source="[&lt;strong&gt;NdisFreeIoWorkItem&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreeioworkitem)"><strong>NdisFreeIoWorkItem</strong></a>函数应：</p>
<ul>
<li>- 如果 <a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize" data-raw-source="[&lt;em&gt;MiniportInitializeEx&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)"><em>MiniportInitializeEx</em></a> 成功，请在 MPHaltEx 中至少调用一次。</li>
<li>-如果<em>MiniportInitializeEx</em>失败，则在<a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize" data-raw-source="[&lt;em&gt;MiniportInitializeEx&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)"><em>MiniportInitializeEx</em></a>中调用。</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-init-registerinterrupt.md" data-raw-source="[&lt;strong&gt;Init_RegisterInterrupt&lt;/strong&gt;](ndis-init-registerinterrupt.md)"><strong>Init_RegisterInterrupt</strong></a></p></td>
<td align="left"><p>Init_RegisterInterrupt 规则指定，如果在初始化过程中出现问题或在停止微型端口驱动程序的过程中出现问题，则必须撤消在初始化期间发生的中断的注册。</p>
<p>如果在<strong>MiniportInitializeEx</strong>期间至少调用了一次<strong>NdisMRegisterInterruptEx</strong> ，则必须在<strong>MiniportHaltEx</strong>中至少调用一次<strong>NdisMDeregisterInterruptEx</strong>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-init-registersg.md" data-raw-source="[&lt;strong&gt;Init_RegisterSG&lt;/strong&gt;](ndis-init-registersg.md)"><strong>Init_RegisterSG</strong></a></p></td>
<td align="left"><p>Init_RegisterSG 规则指定在初始化过程中或在停止微型端口驱动程序的过程中出现错误时，必须撤消在初始化期间 (SG) 的分散收集列表的注册。</p>
<p>如果在<strong>MiniportInitializeEx</strong>期间至少调用了一次<strong>NdisMRegisterScatterGatherDma</strong> ，则<strong>NdisMDeregisterScatterGatherDma</strong>函数应在<strong>MiniportHaltEx</strong>中至少调用一次。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndisfderegisterfilterdriver.md" data-raw-source="[&lt;strong&gt;NdisFDeregisterFilterDriver&lt;/strong&gt;](ndis-ndisfderegisterfilterdriver.md)"><strong>NdisFDeregisterFilterDriver</strong></a></p></td>
<td align="left"><p>筛选器驱动程序必须从其<a href="/windows-hardware/drivers/network/unloading-a-filter-driver" data-raw-source="[&lt;strong&gt;FilterDriverUnload&lt;/strong&gt;](../network/unloading-a-filter-driver.md)"><strong>FilterDriverUnload</strong></a>例程调用<a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfderegisterfilterdriver" data-raw-source="[&lt;strong&gt;NdisFDeregisterFilterDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfderegisterfilterdriver)"><strong>NdisFDeregisterFilterDriver</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndismderegisterinterruptex.md" data-raw-source="[&lt;strong&gt;NdisMDeregisterInterruptEx&lt;/strong&gt;](ndis-ndismderegisterinterruptex.md)"><strong>NdisMDeregisterInterruptEx</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterinterruptex" data-raw-source="[&lt;strong&gt;NdisMDeregisterInterruptEx&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterinterruptex)"><strong>NdisMDeregisterInterruptEx</strong></a>返回 control 后，微型端口驱动程序无法调用<a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsynchronizewithinterruptex" data-raw-source="[&lt;strong&gt;NdisMSynchronizeWithInterruptEx&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsynchronizewithinterruptex)"><strong>NdisMSynchronizeWithInterruptEx</strong></a>函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="nullcheckn.md" data-raw-source="[&lt;strong&gt;NullCheck&lt;/strong&gt;](nullcheckn.md)"><strong>NullCheck</strong></a></p></td>
<td align="left"><p>NullCheck 规则验证驱动程序代码中的 NULL 值是否在稍后的驱动程序中未被引用。 如果满足以下任一条件，则此规则将报告缺陷：</p>
<ul>
<li>指定的值为 NULL，稍后取消引用。</li>
<li>驱动程序中有一个全局/参数，该过程在后面可能为 NULL 的情况下，在该驱动程序中有一个明确的检查，表示指针的初始值可能为 NULL。</li>
</ul>
<p>对于 NullCheck 规则冲突，最相关的代码语句在跟踪树窗格中突出显示。 有关使用报表输出的详细信息，请参阅 <a href="/windows-hardware/drivers/devtest/static-driver-verifier-report" data-raw-source="[Static Driver Verifier Report](./static-driver-verifier-report.md)">静态驱动程序验证程序报表</a> 和 <a href="/windows-hardware/drivers/devtest/understanding-the-defect-viewer" data-raw-source="[Understanding the Trace Viewer](./understanding-the-defect-viewer.md)">了解跟踪查看器</a>。</p>
<p></p></td>
</tr>
</tbody>
</table>

 

**选择 DDI 使用规则集**

1.  选择你的驱动程序项目 () 在 Microsoft Visual Studio 中。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

2.  单击 " **规则** " 选项卡。在 " **规则集**" 下，选择 **DDIUsage**。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请使用 **/check**选项指定**DDIUsage。 sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:DDIUsage.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md) 和 [静态驱动程序验证程序命令 (MSBuild) ](./-static-driver-verifier-commands--msbuild-.md)。

