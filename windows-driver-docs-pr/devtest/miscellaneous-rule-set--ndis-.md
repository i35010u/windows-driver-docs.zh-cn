---
title: 其他规则集 (NDIS)
description: 使用这些规则来验证驱动程序是否正确遵循了对计时器、暂停操作、键、字符串和绑定的正确处理的一组一般要求。
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: b452e73abe04730cc0073b8276fe08e9d46dba88
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839123"
---
# <a name="miscellaneous-rule-set-ndis"></a>其他规则集 (NDIS)


使用这些规则来验证驱动程序是否正确遵循了对计时器、暂停操作、键、字符串和绑定的正确处理的一组一般要求。

## <a name="in-this-section"></a>在本节中


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
<td align="left"><p><a href="ndis-canceltimerobject.md" data-raw-source="[&lt;strong&gt;CancelTimerObject&lt;/strong&gt;](ndis-canceltimerobject.md)"><strong>CancelTimerObject</strong></a></p></td>
<td align="left"><p><a href="ndis-canceltimerobject.md" data-raw-source="[&lt;strong&gt;CancelTimerObject&lt;/strong&gt;](ndis-canceltimerobject.md)"><strong>CancelTimerObject</strong></a>规则指定按替代顺序调用<a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissettimerobject" data-raw-source="[&lt;strong&gt;NdisSetTimerObject&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissettimerobject)"><strong>NdisSetTimerObject</strong></a>和<a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceltimerobject" data-raw-source="[&lt;strong&gt;NdisCancelTimerObject&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceltimerobject)"><strong>NdisCancelTimerObject</strong></a> 。 最终的目标是确保在 <a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)"><em>MiniportHaltEx</em></a> 结束时取消所有计时器。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-miniportpause-return.md" data-raw-source="[&lt;strong&gt;MiniportPause_Return&lt;/strong&gt;](ndis-miniportpause-return.md)"><strong>MiniportPause_Return</strong></a></p></td>
<td align="left"><p><a href="ndis-miniportpause-return.md" data-raw-source="[&lt;strong&gt;MiniportPause_Return&lt;/strong&gt;](ndis-miniportpause-return.md)"><strong>MiniportPause_Return</strong></a>规则指定，如果暂停操作完成，则<a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause" data-raw-source="[&lt;em&gt;MiniportPause&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause)"><em>MiniportPause</em></a>回调函数应仅返回 NDIS_STATUS_SUCCESS; 如果微型端口驱动程序处于暂停状态，则为 NDIS_STATUS_PENDING。 任何其他返回的状态均无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndisopenconfigurationex.md" data-raw-source="[&lt;strong&gt;NdisOpenConfigurationEx&lt;/strong&gt;](ndis-ndisopenconfigurationex.md)"><strong>NdisOpenConfigurationEx</strong></a></p></td>
<td align="left"><p>此规则检查是否按替代顺序调用 <a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenconfigurationex" data-raw-source="[&lt;strong&gt;NdisOpenConfigurationEx&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenconfigurationex)"><strong>NdisOpenConfigurationEx</strong></a> 和 <a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseconfiguration" data-raw-source="[&lt;strong&gt;NdisCloseConfiguration&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseconfiguration)"><strong>NdisCloseConfiguration</strong></a> 。 最终目标是确保在 <a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)"><em>MiniportHaltEx</em></a> 退出后关闭配置句柄</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndisquerybindinstancename.md" data-raw-source="[&lt;strong&gt;NdisQueryBindInstanceName&lt;/strong&gt;](ndis-ndisquerybindinstancename.md)"><strong>NdisQueryBindInstanceName</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisquerybindinstancename" data-raw-source="[&lt;strong&gt;NdisQueryBindInstanceName&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisquerybindinstancename)"><strong>NdisQueryBindInstanceName</strong></a> 为指定友好名称的字符串分配内存。 调用方完成使用此内存后，调用方必须调用 <a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreememory" data-raw-source="[&lt;strong&gt;NdisFreeMemory&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreememory)"><strong>NdisFreeMemory</strong></a> 函数以释放内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndisreenumerateprotocolbindings.md" data-raw-source="[&lt;strong&gt;NdisReEnumerateProtocolBindings&lt;/strong&gt;](ndis-ndisreenumerateprotocolbindings.md)"><strong>NdisReEnumerateProtocolBindings</strong></a></p></td>
<td align="left"><p>协议驱动程序无法从<a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex" data-raw-source="[&lt;em&gt;ProtocolBindAdapterEx&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)"><em>ProtocolBindAdapterEx</em></a>或<a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex" data-raw-source="[&lt;em&gt;ProtocolUnbindAdapterEx&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)"><em>ProtocolUnbindAdapterEx</em></a>函数的上下文中调用<a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreenumerateprotocolbindings" data-raw-source="[&lt;strong&gt;NdisReEnumerateProtocolBindings&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreenumerateprotocolbindings)"><strong>NdisReEnumerateProtocolBindings</strong></a> 。 此外，如果<em>ProtocolNetPnPEvent</em>的<em>ProtocolBindingContext</em>参数不为 NULL，则协议驱动程序无法从<a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event" data-raw-source="[&lt;em&gt;ProtocolNetPnPEvent&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)"><em>ProtocolNetPnPEvent</em></a>函数的上下文中调用<strong>NdisReEnumerateProtocolBindings</strong> 。 但是，如果<em>ProtocolBindingContext</em>为 NULL，则协议驱动程序可以在<em>ProtocolNetPnPEvent</em>的上下文中调用<strong>NdisReEnumerateProtocolBindings</strong> 。 空的 <em>ProtocolBindingContext</em> 值指示该事件适用于所有绑定。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-periodictimer.md" data-raw-source="[&lt;strong&gt;PeriodicTimer&lt;/strong&gt;](ndis-periodictimer.md)"><strong>PeriodicTimer</strong></a></p></td>
<td align="left"><p><a href="ndis-periodictimer.md" data-raw-source="[&lt;strong&gt;PeriodicTimer&lt;/strong&gt;](ndis-periodictimer.md)"><strong>PeriodicTimer</strong></a>规则指定，如果在<a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissettimerobject" data-raw-source="[&lt;strong&gt;NdisSetTimerObject&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissettimerobject)"><strong>NdisSetTimerObject</strong></a>函数的<em>MillisecondsPeriod</em>参数中指定了非零值，则必须在<strong>IRQL = PASSIVE_LEVEL</strong>上运行<a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceltimerobject" data-raw-source="[&lt;strong&gt;NdisCancelTimerObject&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceltimerobject)"><strong>NdisCancelTimerObject</strong></a>的调用方。 如果<strong>NdisSetTimerObject</strong>函数的<em>MillisecondsPeriod</em>参数为零，则<strong>NdisCancelTimerObject</strong>的调用方可以在<strong>IRQL &lt; = DISPATCH_LEVEL</strong>上运行。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-writeerrorlog.md" data-raw-source="[&lt;strong&gt;WriteErrorLog&lt;/strong&gt;](ndis-writeerrorlog.md)"><strong>WriteErrorLog</strong></a></p></td>
<td align="left"><p>WriteErrorLog 规则指定在<em>MiniportInitializeEx</em>函数中调用<strong>NdisMAllocateSharedMemory</strong>函数时，如果分配失败，驱动程序还应调用<strong>NdisWriteErrorLogEntry</strong> 。</p></td>
</tr>
</tbody>
</table>

 

**选择杂项规则集**

1.  选择你的驱动程序项目 () 在 Microsoft Visual Studio 中。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

2.  单击 " **规则** " 选项卡。在 " **规则集**" 下，选择 " **杂项**"。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请使用 **/check** 选项指定 **sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Miscellaneous.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md) 和 [静态驱动程序验证程序命令 (MSBuild) ](./-static-driver-verifier-commands--msbuild-.md)。

