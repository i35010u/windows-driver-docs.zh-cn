---
title: IRQL 规则集 (NDIS)
description: 了解如何使用规则 (NDIS) 来验证驱动程序是否在所需的 IRQL 上进行 DDI 调用。 此外，还将了解如何选择 IRQL 规则集。
ms.assetid: EEFEF8E3-8AB8-46AD-A3BD-DA676F8FA786
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9fd653a72a1e7398e5fe284116ffacef94acd127
ms.sourcegitcommit: 372464be981a39781c71049126f36891cb5d0cad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2020
ms.locfileid: "91646133"
---
# <a name="irql-rule-set-ndis"></a>IRQL 规则集 (NDIS)


使用这些规则验证你的驱动程序是否在所需的 IRQL 上进行 DDI 调用。

不遵循 IRQL 规则的驱动程序可能会导致在操作过程中出现严重问题，从而导致死锁情况或计算机崩溃。

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
<td align="left"><p><a href="ndis-flags-irql.md" data-raw-source="[&lt;strong&gt;Flags_Irql&lt;/strong&gt;](ndis-flags-irql.md)"><strong>Flags_Irql</strong></a></p></td>
<td align="left"><p><a href="ndis-flags-irql.md" data-raw-source="[&lt;strong&gt;Flags_Irql&lt;/strong&gt;](ndis-flags-irql.md)"><strong>Flags_Irql</strong></a>规则指定不能在具有指示当前 Irql 的调度级别标志参数的回调函数中调用<strong>KeGetCurrentIrql</strong> 。</p>
<p>正确使用派单级别标志可帮助避免不必要的设置 IRQL 的尝试。 有关如何使用此标志的详细信息，请参阅 <a href="/windows-hardware/drivers/network/dispatch-irql-tracking" data-raw-source="[Dispatch IRQL Tracking](../network/dispatch-irql-tracking.md)">调度 IRQL 跟踪</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-callmanager-function.md" data-raw-source="[&lt;strong&gt;Irql_CallManager_Function&lt;/strong&gt;](ndis-irql-callmanager-function.md)"><strong>Irql_CallManager_Function</strong></a></p></td>
<td align="left"><p><a href="ndis-irql-callmanager-function.md" data-raw-source="[&lt;strong&gt;Irql_CallManager_Function&lt;/strong&gt;](ndis-irql-callmanager-function.md)"><strong>Irql_CallManager_Function</strong></a>规则指定必须在正确的 Irql 级别调用 ndis CALLMANAGER 的 ndis 函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-irql-connection-function.md" data-raw-source="[&lt;strong&gt;Irql_Connection_Function&lt;/strong&gt;](ndis-irql-connection-function.md)"><strong>Irql_Connection_Function</strong></a></p></td>
<td align="left"><p><a href="ndis-irql-connection-function.md" data-raw-source="[&lt;strong&gt;Irql_Connection_Function&lt;/strong&gt;](ndis-irql-connection-function.md)"><strong>Irql_Connection_Function</strong></a>规则指定协议驱动程序的 NDIS 连接函数必须以正确的 Irql 级别进行调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-filter-driver-function.md" data-raw-source="[&lt;strong&gt;Irql_Filter_Driver_Function&lt;/strong&gt;](ndis-irql-filter-driver-function.md)"><strong>Irql_Filter_Driver_Function</strong></a></p></td>
<td align="left"><p>Irql_Filter_Driver_Function 规则指定必须在正确的 IRQL 级别调用筛选器驱动程序的 NDIS 函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-irql-gather-dma-function.md" data-raw-source="[&lt;strong&gt;Irql_Gather_DMA_Function&lt;/strong&gt;](ndis-irql-gather-dma-function.md)"><strong>Irql_Gather_DMA_Function</strong></a></p></td>
<td align="left"><p>Irql_Gather_DMA_Function 规则指定 NDIS 散播/聚集 DMA 函数必须以正确的 IRQL 级别进行调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-im-function.md" data-raw-source="[&lt;strong&gt;Irql_IM_Function&lt;/strong&gt;](ndis-irql-im-function.md)"><strong>Irql_IM_Function</strong></a></p></td>
<td align="left"><p>Irql_IM_Function 规则指定必须在正确的 IRQL 级别调用用于中间 (IM) 驱动程序的 NDIS 函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-irql-interfaces-function.md" data-raw-source="[&lt;strong&gt;Irql_Interfaces_Function&lt;/strong&gt;](ndis-irql-interfaces-function.md)"><strong>Irql_Interfaces_Function</strong></a></p></td>
<td align="left"><p>Irql_Interfaces_Function 规则指定必须在正确的 IRQL 级别调用 NDIS 网络接口函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-interrupt-function.md" data-raw-source="[&lt;strong&gt;Irql_Interrupt_Function&lt;/strong&gt;](ndis-irql-interrupt-function.md)"><strong>Irql_Interrupt_Function</strong></a></p></td>
<td align="left"><p>Irql_Interrupt_Function 规则指定必须在正确的 IRQL 级别调用用于中断的 NDIS 函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-irql-irqlsetting-function.md" data-raw-source="[&lt;strong&gt;Irql_IrqlSetting_Function&lt;/strong&gt;](ndis-irql-irqlsetting-function.md)"><strong>Irql_IrqlSetting_Function</strong></a></p></td>
<td align="left"><p>Irql_IrqlSetting_Function 规则指定必须在正确的 IRQL 级别调用 NDIS 中断宏。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-mcm-function.md" data-raw-source="[&lt;strong&gt;Irql_MCM_Function&lt;/strong&gt;](ndis-irql-mcm-function.md)"><strong>Irql_MCM_Function</strong></a></p></td>
<td align="left"><p><a href="ndis-irql-mcm-function.md" data-raw-source="[&lt;strong&gt;Irql_MCM_Function&lt;/strong&gt;](ndis-irql-mcm-function.md)"><strong>Irql_MCM_Function</strong></a>规则指定必须在正确的 Irql 级别调用用于驱动程序的 NDIS MCM 函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-irql-mco-function.md" data-raw-source="[&lt;strong&gt;Irql_MCO_Function&lt;/strong&gt;](ndis-irql-mco-function.md)"><strong>Irql_MCO_Function</strong></a></p></td>
<td align="left"><p><a href="ndis-irql-mco-function.md" data-raw-source="[&lt;strong&gt;Irql_MCO_Function&lt;/strong&gt;](ndis-irql-mco-function.md)"><strong>Irql_MCO_Function</strong></a>规则指定必须在正确的 Irql 级别调用微型端口驱动程序的 MCO DDIs。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-miniport-driver-function.md" data-raw-source="[&lt;strong&gt;Irql_Miniport_Driver_Function&lt;/strong&gt;](ndis-irql-miniport-driver-function.md)"><strong>Irql_Miniport_Driver_Function</strong></a></p></td>
<td align="left"><p>Irql_Miniport_Driver_Function 规则指定必须在正确的 IRQL 级别调用微型端口驱动程序的 NDIS 函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-irql-miscellaneous-function.md" data-raw-source="[&lt;strong&gt;Irql_Miscellaneous_Function&lt;/strong&gt;](ndis-irql-miscellaneous-function.md)"><strong>Irql_Miscellaneous_Function</strong></a></p></td>
<td align="left"><p>Irql_Miscellaneous_Function 规则指定必须在正确的 IRQL 级别调用 NDIS 函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-netbuffer-function.md" data-raw-source="[&lt;strong&gt;Irql_NetBuffer_Function&lt;/strong&gt;](ndis-irql-netbuffer-function.md)"><strong>Irql_NetBuffer_Function</strong></a></p></td>
<td align="left"><p>Irql_NetBuffer_Function 规则指定必须在正确的 IRQL 级别调用 NET_BUFFER 相关的函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-irql-oid-function.md" data-raw-source="[&lt;strong&gt;Irql_OID_Function&lt;/strong&gt;](ndis-irql-oid-function.md)"><strong>Irql_OID_Function</strong></a></p></td>
<td align="left"><p><a href="ndis-irql-oid-function.md" data-raw-source="[&lt;strong&gt;Irql_OID_Function&lt;/strong&gt;](ndis-irql-oid-function.md)"><strong>Irql_OID_Function</strong></a>规则指定必须在正确的 Irql 级别调用 NDIS OID 请求 DDIs。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-protocol-driver-function.md" data-raw-source="[&lt;strong&gt;Irql_Protocol_Driver_Function&lt;/strong&gt;](ndis-irql-protocol-driver-function.md)"><strong>Irql_Protocol_Driver_Function</strong></a></p></td>
<td align="left"><p>Irql_Protocol_Driver_Function 规则指定必须在正确的 IRQL 级别调用 CoNDIS 客户端的 NDIS 函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-irql-sendrcv-function.md" data-raw-source="[&lt;strong&gt;Irql_SendRcv_Function&lt;/strong&gt;](ndis-irql-sendrcv-function.md)"><strong>Irql_SendRcv_Function</strong></a></p></td>
<td align="left"><p><a href="ndis-irql-sendrcv-function.md" data-raw-source="[&lt;strong&gt;Irql_SendRcv_Function&lt;/strong&gt;](ndis-irql-sendrcv-function.md)"><strong>Irql_SendRcv_Function</strong></a>规则指定必须在正确的 Irql 级别调用 NDIS 驱动程序的发送和接收功能。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-statusindication-function.md" data-raw-source="[&lt;strong&gt;Irql_StatusIndication_Function&lt;/strong&gt;](ndis-irql-statusindication-function.md)"><strong>Irql_StatusIndication_Function</strong></a></p></td>
<td align="left"><p>Irql_StatusIndication_Function 规则指定必须在正确的 IRQL 级别调用微型端口和筛选器驱动程序的 NDIS 状态指示函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-irql-synch-function.md" data-raw-source="[&lt;strong&gt;Irql_Synch_Function&lt;/strong&gt;](ndis-irql-synch-function.md)"><strong>Irql_Synch_Function</strong></a></p></td>
<td align="left"><p><a href="ndis-irql-synch-function.md" data-raw-source="[&lt;strong&gt;Irql_Synch_Function&lt;/strong&gt;](ndis-irql-synch-function.md)"><strong>Irql_Synch_Function</strong></a>规则指定必须在正确的 Irql 级别调用 NDIS 中断和同步 DDIs。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-timer-function.md" data-raw-source="[&lt;strong&gt;Irql_Timer_Function&lt;/strong&gt;](ndis-irql-timer-function.md)"><strong>Irql_Timer_Function</strong></a></p></td>
<td align="left"><p>Irql_Timer_Function 规则指定必须在正确的 IRQL 级别调用 NDIS Timer 服务函数。</p></td>
</tr>
</tbody>
</table>

 

**选择 Irql 规则集**

1.  选择你的驱动程序项目 () 在 Microsoft Visual Studio 中。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

2.  单击 " **规则** " 选项卡。在 " **规则集**" 下，选择 **Irql**。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请将 **sdv** 与 **/check** 选项一起指定。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Irql.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md) 和 [静态驱动程序验证程序命令 (MSBuild) ](./-static-driver-verifier-commands--msbuild-.md)。

