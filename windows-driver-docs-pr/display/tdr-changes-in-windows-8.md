---
title: Windows 8 中的 TDR 更改
description: 从 Windows 8 开始，GPU 超时检测和恢复 (TDR) 行为已更改为允许重置各个物理适配器的各个部分，而不需要进行适配器范围的重置。
ms.assetid: 5BC4F94C-2B45-44E2-8BBF-B455BB864A29
keywords:
- TDR (超时检测和恢复) WDK 显示，Windows 8 中的更改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df08337a2e9e156eab053e57445cd162e0ed5328
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105686"
---
# <a name="tdr-changes-in-windows-8"></a>Windows 8 中的 TDR 更改


从 Windows 8 开始，GPU 超时检测和恢复 (TDR) 行为已更改为允许重置各个物理适配器的各个部分，而不需要进行适配器范围的重置。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">最小 Windows 显示器驱动程序模型 (WDDM) 版本</td>
<td align="left">1.2</td>
</tr>
<tr class="even">
<td align="left">最大 Windows 版本</td>
<td align="left">8</td>
</tr>
<tr class="odd">
<td align="left">驱动程序实现-仅限完整图形和呈现</td>
<td align="left">必需</td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/test/hlk/windows-hardware-lab-kit" data-raw-source="[WHCK](/windows-hardware/test/hlk/windows-hardware-lab-kit)">WHCK</a> 要求和测试</td>
<td align="left"><p><strong>设备 .。。TDRResiliency</strong></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idtdr_device_driver_interface__ddi_spanspan-idtdr_device_driver_interface__ddi_spanspan-idtdr_device_driver_interface__ddi_spantdr-device-driver-interface-ddi"></a><span id="TDR_device_driver_interface__DDI_"></span><span id="tdr_device_driver_interface__ddi_"></span><span id="TDR_DEVICE_DRIVER_INTERFACE__DDI_"></span>TDR 设备驱动程序接口 (DDI) 


为了适应此行为更改，显示微型端口驱动程序应实现以下功能：

-   [*DxgkDdiQueryDependentEngineGroup*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_querydependentenginegroup)
-   [*DxgkDdiQueryEngineStatus*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryenginestatus)
-   [*DxgkDdiResetEngine*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetengine)

**注意**   支持这些函数的驱动程序也必须支持对[*DxgkDdiCollectDbgInfo*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_collectdbginfo)函数进行级别0同步。 这是为了确保不会影响级别零微型端口调用，重置操作可以继续执行。 请参阅 *DxgkDdiCollectDbgInfo*的备注。

 

这些结构与新函数关联：

-   [**DXGK \_DRIVERCAPS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps) (New **SupportPerEngineTDR** 成员) 
-   [**DXGK \_ ENGINESTATUS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_enginestatus)
-   [**DXGKARG \_ QUERYDEPENDENTENGINEGROUP**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_querydependentenginegroup)
-   [**DXGKARG \_ QUERYENGINESTATUS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryenginestatus)
-   [**DXGKARG \_ RESETENGINE**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_resetengine)

显示微型端口驱动程序通过设置 [**DXGK \_ DRIVERCAPS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)指示支持这些函数。**SupportPerEngineTDR** 成员，在这种情况下，它必须实现 [*DxgkDdiQueryDependentEngineGroup*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_querydependentenginegroup)、 [*DxgkDdiQueryEngineStatus*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryenginestatus)和 [*DxgkDdiResetEngine*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetengine) 函数。

## <a name="span-idtdr_process_descriptionspanspan-idtdr_process_descriptionspanspan-idtdr_process_descriptionspantdr-process-description"></a><span id="TDR_process_description"></span><span id="tdr_process_description"></span><span id="TDR_PROCESS_DESCRIPTION"></span>TDR 进程说明


当系统在处理最终用户命令或操作时出现完全冻结或挂起时，图形中会出现常见的稳定性问题。 通常，GPU 是繁忙的处理密集型图形操作，通常在游戏播放期间。 不会进行屏幕更新，用户假定其系统已冻结。 用户通常会等待几秒钟，并按下 "电源" 按钮重新启动系统。

Windows Vista 和 Windows 7 都尝试检测这些问题挂起情况并动态恢复响应式桌面。 系统不会重新启动，但在大多数情况下，屏幕会闪烁。 但是，某些较旧的 Microsoft DirectX 应用程序会在恢复结束时呈现黑屏，用户必须重新启动这些应用程序。 这些 GPU 挂起称为超时检测和恢复错误 (Tdr) 。

此图显示了超时检测和恢复过程。 有关此过程的更多详细信息，请参阅 [超时检测和恢复 (TDR) ](timeout-detection-and-recovery.md)。

![超时检测和恢复 (通过 wddm 进行的 gpu) tdr](images/timeoutdetectionrecoverygpusthroughwddm.jpg)

当 GPU 命令完成时间太长或硬件挂起时，会发生 Tdr。 Tdr 使操作系统能够检测 UI 没有响应。

## <a name="span-idnodesspanspan-idnodesspanspan-idnodesspannodes"></a><span id="Nodes"></span><span id="nodes"></span><span id="NODES"></span>结点


正如上面的 TDR 函数所使用的那样， *节点* 是单个物理适配器的多个部件中的一个，可以单独进行计划。 例如，3-d 节点、视频解码节点和复制节点都可以存在于同一物理适配器中，每个节点都可以在[**DXGKARG \_ QUERYDEPENDENTENGINEGROUP**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_querydependentenginegroup)中为每个节点指定一个单独的节点序号值。**NodeOrdinal**对[*DxgkDdiQueryDependentEngineGroup*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_querydependentenginegroup)的调用中的 NodeOrdinal 成员。

物理适配器中的节点数由[**DXGK \_ DRIVERCAPS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)的**NbAsymetricProcessingNodes**成员中的显示微型端口驱动程序报告。**GpuEngineTopology**。

创建上下文时，将在[**DXGKARG \_ CREATECONTEXT**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_createcontext)结构的**NodeOrdinal**成员中传递节点序号值。

## <a name="span-idenginesspanspan-idenginesspanspan-idenginesspanengines"></a><span id="Engines"></span><span id="engines"></span><span id="ENGINES"></span>增多


正如上面的 TDR 函数中所使用的那样， *引擎* 是) 的多个物理适配器 (或 gpu，它们共同充当一个逻辑适配器。 DirectX 图形内核子系统支持此类配置，但要求每个引擎必须具有相同数目的节点。

例如，GPU 计划程序将引擎0视为与物理适配器0相对应。 引擎0的节点数必须与与适配器1对应的引擎1的节点数相同。

## <a name="span-idengine_ordinal_value_at_context_creationspanspan-idengine_ordinal_value_at_context_creationspanspan-idengine_ordinal_value_at_context_creationspanengine-ordinal-value-at-context-creation"></a><span id="Engine_ordinal_value_at_context_creation"></span><span id="engine_ordinal_value_at_context_creation"></span><span id="ENGINE_ORDINAL_VALUE_AT_CONTEXT_CREATION"></span>上下文创建时的引擎序号值


创建上下文时，将在[**DXGKARG \_ CREATECONTEXT**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_createcontext)结构的**EngineAffinity**成员中设置与引擎序号值相对应的单个位。 此和其他计划程序相关结构的 **EngineOrdinal** 成员是从零开始的索引。 **EngineAffinity**的值为 1 &lt; &lt; **EngineOrdinal**，而**EngineOrdinal**是**EngineAffinity**中的最大数位。

## <a name="span-idpackets_unaffected_by_engine_resetspanspan-idpackets_unaffected_by_engine_resetspanspan-idpackets_unaffected_by_engine_resetspanpackets-unaffected-by-engine-reset"></a><span id="Packets_unaffected_by_engine_reset"></span><span id="packets_unaffected_by_engine_reset"></span><span id="PACKETS_UNAFFECTED_BY_ENGINE_RESET"></span>不受引擎重置影响的数据包


GPU 计划程序可能会要求该驱动程序将提交时间太迟于引擎硬件队列的数据包重新提交到引擎硬件队列，以便在完成引擎重置之前进行完全处理。 驱动程序必须遵循以下准则才能重新提交此类数据包：

-   *分页数据包*： GPU 计划程序将要求驱动程序使用其原始防护 id 重新提交寻呼包，其顺序与最初提交时相同。 在将新数据包添加到硬件队列之前，将重新提交所有此类数据包。
-   *呈现数据包*： GPU 计划程序会将呈现数据包分配给新的防护 id，然后重新提交。

## <a name="span-idcalling_sequence_to_reset_an_enginespanspan-idcalling_sequence_to_reset_an_enginespanspan-idcalling_sequence_to_reset_an_enginespancalling-sequence-to-reset-an-engine"></a><span id="Calling_sequence_to_reset_an_engine"></span><span id="calling_sequence_to_reset_an_engine"></span><span id="CALLING_SEQUENCE_TO_RESET_AN_ENGINE"></span>调用序列以重置引擎


当 [*DxgkDdiResetEngine*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetengine) 成功时，GPU 计划程序确保从引擎重置调用返回的 **LastAbortedFenceId** 值对应于硬件队列中的现有防护 id 或 GPU 上最后完成的隔离 id。 当在检测到 GPU 超时后，但在调用引擎重置回调之前，会发生后一种情况。

GPU 上最后完成的防护 ID 值必须始终由驱动程序维护，因为还需要设置 **DmaPreempted**。DXGKARGCB 的**LastCompletedFenceId** 成员 [** \_ 通知 \_ 中断 \_ 数据**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkargcb_notify_interrupt_data) 抢占中断通知结构。 在以下情况下，最后完成的防护 ID 应为 "高级"：

-   当数据包完成后 (未抢占) 时，最后完成的防护 ID 应该设置为已完成数据包的防护 ID。
-   当 [*DxgkDdiResetEngine*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetengine) 成功时，最后一个已完成的防护 ID 应该设置为由引擎重置调用返回的 **LastCompletedFenceId** 成员的值。
-   对于适配器范围内的重置，所有节点上最后完成的防护 ID 都应提前到重置时的上次提交的防护 ID。

下面是由 GPU 计划程序发现的成功重置引擎的时间顺序：

1.  发出了一个抢占尝试。
2.  检测到 GPU 超时。
3.  GPU 计划程序会获取最后提交和已完成的防护 Id 的快照，并忽略来自超时引擎的中断。 这是设备中断级别的一个原子操作。
4.  如果此时硬件队列中没有数据包，请退出。 如果在步骤2和3之间的时间范围内完成了包，则可能会发生这种情况。
5.  所有排队 Dpc 都将刷新。
6.  准备引擎重置。
7.  调用 [*DxgkDdiResetEngine*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetengine)。
8.  如果 **LastAbortedFenceId** 成员小于最后一个已完成的防护 id 或大于最后提交的防护 id，则 DirectX 图形内核子系统将导致发生系统检查错误。 在故障转储文件中，消息错误 **检查 0x119**会记录错误，该错误具有以下四个参数：
    -   0xA，表示驱动程序报告了无效的已中止的防护 ID
    -   驱动程序返回的**LastAbortedFenceId**值
    -   上次完成的防护 ID
    -   内部操作系统参数

9.  如果 **LastAbortedFenceId** 值有效，则继续执行引擎重置恢复，如下所示。 如果对分页数据包的重置受到了影响，则 GPU 计划程序会在发生适配器范围重置时执行引擎重置。 所有拥有此寻呼数据包引用的分配的设备也会置于错误状态。 但是，系统设备本身并不会进入错误状态，它将在重置完成之后继续执行。

## <a name="span-idspecial_casesspanspan-idspecial_casesspanspan-idspecial_casesspanspecial-cases"></a><span id="Special_cases"></span><span id="special_cases"></span><span id="SPECIAL_CASES"></span>特殊情况


在上述步骤3和步骤7之间的 GPU 上完成数据包时，可能会出现一种特殊情况。 在这种情况下，如果从驱动程序的角度来看， **LastAbortedFenceId** 应由驱动程序设置为最后完成的数据包的防护 ID。 从计划程序的角度来看，它会显示此类数据包被中止，并且相应的设备将处于错误状态，即使数据包最终完成也是如此。

如果驱动程序无法执行重置操作，原因是硬件处于无效状态，或硬件无法重置节点，则驱动程序应返回失败状态代码。 如果 GPU 计划程序收到故障状态代码，则它会按照 Windows 8 之前的 [TDR 行为](timeout-detection-and-recovery.md) 执行适配器范围的重置和重启操作。

即使驱动程序已选择进入 Windows 8 TDR 行为，在某些情况下，GPU 计划程序会请求重置并重新启动整个逻辑适配器。 因此，驱动程序仍必须实现 [*DxgkDdiResetFromTimeout*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout) 和 [*DxgkDdiRestartFromTimeout*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_restartfromtimeout) 函数，并且它们的语义与 Windows 8 之前的语义保持不变。 当尝试使用 [*DxgkDdiResetEngine*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetengine) 重置物理适配器时，会导致逻辑适配器重置，Windows 调试器的 " **！分析** " 命令显示 TDR 恢复上下文的 **TdrReason** 值设置为新值 **TdrEngineTimeoutPromotedToAdapterReset** = 9。

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


有关硬件设备实现此功能时必须满足的要求的信息，请参阅相关 [WHCK 文档](/windows-hardware/test/hlk/windows-hardware-lab-kit) **TDRResiliency**。

请参阅 [WDDM 1.2 功能](wddm-v1-2-features.md) ，了解 Windows 8 中添加的功能。

