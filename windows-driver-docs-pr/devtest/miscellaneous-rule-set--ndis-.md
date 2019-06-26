---
title: 其他规则集 (NDIS)
description: 使用这些规则来验证您的驱动程序正确地遵循一组常规的计时器、 暂停操作、 密钥、 字符串和绑定要求正确处理。
ms.assetid: 2F4A68DB-7619-4F36-8FA1-C9350604FDED
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: adc285a3671287e2f85f232261e6d4ae762c42b8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361295"
---
# <a name="miscellaneous-rule-set-ndis"></a>其他规则集 (NDIS)


使用这些规则来验证您的驱动程序正确地遵循一组常规的计时器、 暂停操作、 密钥、 字符串和绑定要求正确处理。

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
<td align="left"><p><a href="ndis-canceltimerobject.md" data-raw-source="[&lt;strong&gt;CancelTimerObject&lt;/strong&gt;](ndis-canceltimerobject.md)"><strong>CancelTimerObject</strong></a></p></td>
<td align="left"><p><a href="ndis-canceltimerobject.md" data-raw-source="[&lt;strong&gt;CancelTimerObject&lt;/strong&gt;](ndis-canceltimerobject.md)"> <strong>CancelTimerObject</strong> </a>规则指定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissettimerobject" data-raw-source="[&lt;strong&gt;NdisSetTimerObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissettimerobject)"> <strong>NdisSetTimerObject</strong> </a>并<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscanceltimerobject" data-raw-source="[&lt;strong&gt;NdisCancelTimerObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscanceltimerobject)"> <strong>NdisCancelTimerObject</strong> </a>备用顺序调用。 最终目标是确保所有计时器将被都取消时<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)"> <em>MiniportHaltEx</em> </a>结束。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-miniportpause-return.md" data-raw-source="[&lt;strong&gt;MiniportPause_Return&lt;/strong&gt;](ndis-miniportpause-return.md)"><strong>MiniportPause_Return</strong></a></p></td>
<td align="left"><p><a href="ndis-miniportpause-return.md" data-raw-source="[&lt;strong&gt;MiniportPause_Return&lt;/strong&gt;](ndis-miniportpause-return.md)"> <strong>MiniportPause_Return</strong> </a>规则指定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pause" data-raw-source="[&lt;em&gt;MiniportPause&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pause)"> <em>MiniportPause</em> </a>回调函数应返回仅 NDIS_STATUS_如果暂停操作已完成，则为 SUCCESS 或 NDIS_STATUS_PENDING 微型端口驱动程序是否处于暂停状态。 其他任何返回的状态无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndisopenconfigurationex.md" data-raw-source="[&lt;strong&gt;NdisOpenConfigurationEx&lt;/strong&gt;](ndis-ndisopenconfigurationex.md)"><strong>NdisOpenConfigurationEx</strong></a></p></td>
<td align="left"><p>此规则检查<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisopenconfigurationex" data-raw-source="[&lt;strong&gt;NdisOpenConfigurationEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisopenconfigurationex)"> <strong>NdisOpenConfigurationEx</strong> </a>并<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscloseconfiguration" data-raw-source="[&lt;strong&gt;NdisCloseConfiguration&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscloseconfiguration)"> <strong>NdisCloseConfiguration</strong> </a>备用顺序调用。 请确保配置句柄已关闭时的最终目标是<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)"> <em>MiniportHaltEx</em> </a>退出</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndisquerybindinstancename.md" data-raw-source="[&lt;strong&gt;NdisQueryBindInstanceName&lt;/strong&gt;](ndis-ndisquerybindinstancename.md)"><strong>NdisQueryBindInstanceName</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisquerybindinstancename" data-raw-source="[&lt;strong&gt;NdisQueryBindInstanceName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisquerybindinstancename)"><strong>NdisQueryBindInstanceName</strong> </a>为指定的友好名称的字符串分配内存。 调用方完成使用此内存后，必须调用调用方<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreememory" data-raw-source="[&lt;strong&gt;NdisFreeMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreememory)"> <strong>NdisFreeMemory</strong> </a>函数，以释放内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndisreenumerateprotocolbindings.md" data-raw-source="[&lt;strong&gt;NdisReEnumerateProtocolBindings&lt;/strong&gt;](ndis-ndisreenumerateprotocolbindings.md)"><strong>NdisReEnumerateProtocolBindings</strong></a></p></td>
<td align="left"><p>协议驱动程序不能调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreenumerateprotocolbindings" data-raw-source="[&lt;strong&gt;NdisReEnumerateProtocolBindings&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreenumerateprotocolbindings)"> <strong>NdisReEnumerateProtocolBindings</strong> </a>中的上下文中<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex" data-raw-source="[&lt;em&gt;ProtocolBindAdapterEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)"> <em>ProtocolBindAdapterEx</em> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_unbind_adapter_ex" data-raw-source="[&lt;em&gt;ProtocolUnbindAdapterEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_unbind_adapter_ex)"> <em>ProtocolUnbindAdapterEx</em> </a>函数。 此外，协议驱动程序不能调用<strong>NdisReEnumerateProtocolBindings</strong>中的上下文中<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event" data-raw-source="[&lt;em&gt;ProtocolNetPnPEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event)"> <em>ProtocolNetPnPEvent</em> </a>函数如果<em>ProtocolBindingContext</em>的参数<em>ProtocolNetPnPEvent</em>不为 NULL。 但是，协议驱动程序可以调用<strong>NdisReEnumerateProtocolBindings</strong>中的上下文中<em>ProtocolNetPnPEvent</em>如果<em>ProtocolBindingContext</em>为 NULL。 为空<em>ProtocolBindingContext</em>值指示该事件适用于所有绑定。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-periodictimer.md" data-raw-source="[&lt;strong&gt;PeriodicTimer&lt;/strong&gt;](ndis-periodictimer.md)"><strong>PeriodicTimer</strong></a></p></td>
<td align="left"><p><a href="ndis-periodictimer.md" data-raw-source="[&lt;strong&gt;PeriodicTimer&lt;/strong&gt;](ndis-periodictimer.md)"> <strong>PeriodicTimer</strong> </a>规则指定的调用方<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscanceltimerobject" data-raw-source="[&lt;strong&gt;NdisCancelTimerObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscanceltimerobject)"> <strong>NdisCancelTimerObject</strong> </a>必须在运行<strong>IRQL =PASSIVE_LEVEL</strong>如果在指定了一个非零值<em>MillisecondsPeriod</em>参数<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissettimerobject" data-raw-source="[&lt;strong&gt;NdisSetTimerObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissettimerobject)"> <strong>NdisSetTimerObject</strong> </a>函数。 如果<em>MillisecondsPeriod</em>的参数<strong>NdisSetTimerObject</strong>函数是零的调用方<strong>NdisCancelTimerObject</strong>可以在运行<strong>IRQL&lt;= DISPATCH_LEVEL</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-writeerrorlog.md" data-raw-source="[&lt;strong&gt;WriteErrorLog&lt;/strong&gt;](ndis-writeerrorlog.md)"><strong>WriteErrorLog</strong></a></p></td>
<td align="left"><p>WriteErrorLog 规则指定，如果<strong>NdisMAllocateSharedMemory</strong>调用函数<em>MiniportInitializeEx</em>函数，该驱动程序还应调用<strong>NdisWriteErrorLogEntry</strong>如果分配失败。</p></td>
</tr>
</tbody>
</table>

 

**若要选择其他规则集**

1.  Microsoft Visual Studio 中选择您的驱动程序项目 (.vcxProj)。 从**驱动程序**菜单上，单击**启动 Static Driver Verifier...** .

2.  单击**规则**选项卡。下**规则集**，选择**杂项**。

    若要选择的默认规则集从 Visual Studio 开发人员命令提示符窗口，请指定**Miscellaneous.sdv**与 **/check**选项。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Miscellaneous.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅[以找到缺陷驱动程序中使用 Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)并[Static Driver Verifier 命令 (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)。

 

 





