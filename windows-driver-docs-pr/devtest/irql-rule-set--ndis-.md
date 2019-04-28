---
title: IRQL 规则集 (NDIS)
description: 使用这些规则来验证您的驱动程序所需的 IRQL 在进行 DDI 调用。未遵循 IRQL 规则的驱动程序可以操作可能会导致死锁条件或计算机崩溃期间导致严重问题。
ms.assetid: EEFEF8E3-8AB8-46AD-A3BD-DA676F8FA786
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4befa47c1344c34329372af6135fe338d563f161
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340464"
---
# <a name="irql-rule-set-ndis"></a>IRQL 规则集 (NDIS)


使用这些规则来验证您的驱动程序所需的 IRQL 在进行 DDI 调用。

未遵循 IRQL 规则的驱动程序可以操作可能会导致死锁条件或计算机崩溃期间导致严重问题。

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
<td align="left"><p><a href="ndis-flags-irql.md" data-raw-source="[&lt;strong&gt;Flags_Irql&lt;/strong&gt;](ndis-flags-irql.md)"><strong>Flags_Irql</strong></a></p></td>
<td align="left"><p><a href="ndis-flags-irql.md" data-raw-source="[&lt;strong&gt;Flags_Irql&lt;/strong&gt;](ndis-flags-irql.md)"> <strong>Flags_Irql</strong> </a>规则指定<strong>KeGetCurrentIrql</strong>不必须具有一个调度级别标志参数，指示的回调函数内调用当前 IRQL。</p>
<p>正确使用调度级别标志可以帮助您避免不必要的尝试设置 IRQL。 有关如何使用此标志的详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff546448" data-raw-source="[Dispatch IRQL Tracking](https://msdn.microsoft.com/library/windows/hardware/ff546448)">调度 IRQL 跟踪</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-callmanager-function.md" data-raw-source="[&lt;strong&gt;Irql_CallManager_Function&lt;/strong&gt;](ndis-irql-callmanager-function.md)"><strong>Irql_CallManager_Function</strong></a></p></td>
<td align="left"><p><a href="ndis-irql-callmanager-function.md" data-raw-source="[&lt;strong&gt;Irql_CallManager_Function&lt;/strong&gt;](ndis-irql-callmanager-function.md)"> <strong>Irql_CallManager_Function</strong> </a>规则指定必须在正确的 IRQL 级别上名为 NDIS CallManager 的 NDIS 函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-irql-connection-function.md" data-raw-source="[&lt;strong&gt;Irql_Connection_Function&lt;/strong&gt;](ndis-irql-connection-function.md)"><strong>Irql_Connection_Function</strong></a></p></td>
<td align="left"><p><a href="ndis-irql-connection-function.md" data-raw-source="[&lt;strong&gt;Irql_Connection_Function&lt;/strong&gt;](ndis-irql-connection-function.md)"> <strong>Irql_Connection_Function</strong> </a>规则指定必须在正确的 IRQL 级别调用协议驱动程序的 NDIS 连接函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-filter-driver-function.md" data-raw-source="[&lt;strong&gt;Irql_Filter_Driver_Function&lt;/strong&gt;](ndis-irql-filter-driver-function.md)"><strong>Irql_Filter_Driver_Function</strong></a></p></td>
<td align="left"><p>Irql_Filter_Driver_Function 规则指定必须在正确的 IRQL 级别上名为筛选器驱动程序的 NDIS 函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-irql-gather-dma-function.md" data-raw-source="[&lt;strong&gt;Irql_Gather_DMA_Function&lt;/strong&gt;](ndis-irql-gather-dma-function.md)"><strong>Irql_Gather_DMA_Function</strong></a></p></td>
<td align="left"><p>Irql_Gather_DMA_Function 规则指定的 NDIS 散播-聚集 DMA 函数的调用必须在正确的 IRQL 级别。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-im-function.md" data-raw-source="[&lt;strong&gt;Irql_IM_Function&lt;/strong&gt;](ndis-irql-im-function.md)"><strong>Irql_IM_Function</strong></a></p></td>
<td align="left"><p>Irql_IM_Function 规则指定必须在正确的 IRQL 级别上名为中间 (IM) 驱动程序的 NDIS 函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-irql-interfaces-function.md" data-raw-source="[&lt;strong&gt;Irql_Interfaces_Function&lt;/strong&gt;](ndis-irql-interfaces-function.md)"><strong>Irql_Interfaces_Function</strong></a></p></td>
<td align="left"><p>Irql_Interfaces_Function 规则指定必须在正确的 IRQL 级别上名为的 NDIS 网络接口功能。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-interrupt-function.md" data-raw-source="[&lt;strong&gt;Irql_Interrupt_Function&lt;/strong&gt;](ndis-irql-interrupt-function.md)"><strong>Irql_Interrupt_Function</strong></a></p></td>
<td align="left"><p>Irql_Interrupt_Function 规则指定必须在正确的 IRQL 级别上名为中断的 NDIS 函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-irql-irqlsetting-function.md" data-raw-source="[&lt;strong&gt;Irql_IrqlSetting_Function&lt;/strong&gt;](ndis-irql-irqlsetting-function.md)"><strong>Irql_IrqlSetting_Function</strong></a></p></td>
<td align="left"><p>Irql_IrqlSetting_Function 规则指定必须在正确的 IRQL 级别上名为 NDIS 中断宏。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-mcm-function.md" data-raw-source="[&lt;strong&gt;Irql_MCM_Function&lt;/strong&gt;](ndis-irql-mcm-function.md)"><strong>Irql_MCM_Function</strong></a></p></td>
<td align="left"><p><a href="ndis-irql-mcm-function.md" data-raw-source="[&lt;strong&gt;Irql_MCM_Function&lt;/strong&gt;](ndis-irql-mcm-function.md)"> <strong>Irql_MCM_Function</strong> </a>规则指定必须在正确的 IRQL 级别上名为驱动程序的 NDIS MCM 函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-irql-mco-function.md" data-raw-source="[&lt;strong&gt;Irql_MCO_Function&lt;/strong&gt;](ndis-irql-mco-function.md)"><strong>Irql_MCO_Function</strong></a></p></td>
<td align="left"><p><a href="ndis-irql-mco-function.md" data-raw-source="[&lt;strong&gt;Irql_MCO_Function&lt;/strong&gt;](ndis-irql-mco-function.md)"> <strong>Irql_MCO_Function</strong> </a>规则指定必须在正确的 IRQL 级别上名为 NDIS MCO DDIs 微型端口驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-miniport-driver-function.md" data-raw-source="[&lt;strong&gt;Irql_Miniport_Driver_Function&lt;/strong&gt;](ndis-irql-miniport-driver-function.md)"><strong>Irql_Miniport_Driver_Function</strong></a></p></td>
<td align="left"><p>Irql_Miniport_Driver_Function 规则指定，必须在正确的 IRQL 级别调用微型端口驱动程序的 NDIS 函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-irql-miscellaneous-function.md" data-raw-source="[&lt;strong&gt;Irql_Miscellaneous_Function&lt;/strong&gt;](ndis-irql-miscellaneous-function.md)"><strong>Irql_Miscellaneous_Function</strong></a></p></td>
<td align="left"><p>Irql_Miscellaneous_Function 规则指定必须在正确的 IRQL 级别上名为 NDIS 函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-netbuffer-function.md" data-raw-source="[&lt;strong&gt;Irql_NetBuffer_Function&lt;/strong&gt;](ndis-irql-netbuffer-function.md)"><strong>Irql_NetBuffer_Function</strong></a></p></td>
<td align="left"><p>Irql_NetBuffer_Function 规则指定必须在正确的 IRQL 级别上名为 NET_BUFFER 相关函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-irql-oid-function.md" data-raw-source="[&lt;strong&gt;Irql_OID_Function&lt;/strong&gt;](ndis-irql-oid-function.md)"><strong>Irql_OID_Function</strong></a></p></td>
<td align="left"><p><a href="ndis-irql-oid-function.md" data-raw-source="[&lt;strong&gt;Irql_OID_Function&lt;/strong&gt;](ndis-irql-oid-function.md)"> <strong>Irql_OID_Function</strong> </a>规则指定必须在正确的 IRQL 级别上名为 NDIS OID 请求 DDIs。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-protocol-driver-function.md" data-raw-source="[&lt;strong&gt;Irql_Protocol_Driver_Function&lt;/strong&gt;](ndis-irql-protocol-driver-function.md)"><strong>Irql_Protocol_Driver_Function</strong></a></p></td>
<td align="left"><p>Irql_Protocol_Driver_Function 规则指定必须在正确的 IRQL 级别上名为的 CoNDIS 客户端的 NDIS 函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-irql-sendrcv-function.md" data-raw-source="[&lt;strong&gt;Irql_SendRcv_Function&lt;/strong&gt;](ndis-irql-sendrcv-function.md)"><strong>Irql_SendRcv_Function</strong></a></p></td>
<td align="left"><p><a href="ndis-irql-sendrcv-function.md" data-raw-source="[&lt;strong&gt;Irql_SendRcv_Function&lt;/strong&gt;](ndis-irql-sendrcv-function.md)"> <strong>Irql_SendRcv_Function</strong> </a>规则指定发送和接收的 NDIS 驱动程序必须在正确的 IRQL 级别调用函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-statusindication-function.md" data-raw-source="[&lt;strong&gt;Irql_StatusIndication_Function&lt;/strong&gt;](ndis-irql-statusindication-function.md)"><strong>Irql_StatusIndication_Function</strong></a></p></td>
<td align="left"><p>Irql_StatusIndication_Function 规则指定，必须在正确的 IRQL 级别调用微型端口和筛选器驱动程序的 NDIS 状态指示函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-irql-synch-function.md" data-raw-source="[&lt;strong&gt;Irql_Synch_Function&lt;/strong&gt;](ndis-irql-synch-function.md)"><strong>Irql_Synch_Function</strong></a></p></td>
<td align="left"><p><a href="ndis-irql-synch-function.md" data-raw-source="[&lt;strong&gt;Irql_Synch_Function&lt;/strong&gt;](ndis-irql-synch-function.md)"> <strong>Irql_Synch_Function</strong> </a>规则指定的 NDIS 中断和同步 DDIs 必须调用在正确的 IRQL 级别。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-irql-timer-function.md" data-raw-source="[&lt;strong&gt;Irql_Timer_Function&lt;/strong&gt;](ndis-irql-timer-function.md)"><strong>Irql_Timer_Function</strong></a></p></td>
<td align="left"><p>Irql_Timer_Function 规则指定必须在正确的 IRQL 级别上名为的 NDIS 计时器服务功能。</p></td>
</tr>
</tbody>
</table>

 

**若要选择的 Irql 规则设置**

1.  Microsoft Visual Studio 中选择您的驱动程序项目 (.vcxProj)。 从**驱动程序**菜单上，单击**启动 Static Driver Verifier...**.

2.  单击**规则**选项卡。下**规则集**，选择**Irql**。

    若要选择的默认规则集从 Visual Studio 开发人员命令提示符窗口，请指定**Irql.sdv**与 **/check**选项。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Irql.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅[以找到缺陷驱动程序中使用 Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/hh454281)并[Static Driver Verifier 命令 (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)。

 

 





