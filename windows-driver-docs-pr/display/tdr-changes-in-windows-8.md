---
title: Windows 8 中的 TDR 更改
description: 从 Windows 8，GPU 超时检测和恢复 (TDR) 行为已更改为允许单个物理适配器，以重置，而不是要求适配器范围重置的部分。
ms.assetid: 5BC4F94C-2B45-44E2-8BBF-B455BB864A29
keywords:
- （超时检测和恢复） TDR WDK 显示，Windows 8 中的更改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a7ad0cd9205de14e01b4ccb197090c856f68298
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562872"
---
# <a name="tdr-changes-in-windows-8"></a>Windows 8 中的 TDR 更改


从 Windows 8，GPU 超时检测和恢复 (TDR) 行为已更改为允许单个物理适配器，以重置，而不是要求适配器范围重置的部分。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">Windows 显示器驱动程序模型 (WDDM) 的最低版本</td>
<td align="left">1.2</td>
</tr>
<tr class="even">
<td align="left">最大 Windows 版本</td>
<td align="left">8</td>
</tr>
<tr class="odd">
<td align="left">驱动程序实现 — 仅完全图形和呈现</td>
<td align="left">强制</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit" data-raw-source="[WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)">WHCK</a>要求和测试</td>
<td align="left"><p><strong>Device.Graphics…TDRResiliency</strong></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idtdrdevicedriverinterfaceddispanspan-idtdrdevicedriverinterfaceddispanspan-idtdrdevicedriverinterfaceddispantdr-device-driver-interface-ddi"></a><span id="TDR_device_driver_interface__DDI_"></span><span id="tdr_device_driver_interface__ddi_"></span><span id="TDR_DEVICE_DRIVER_INTERFACE__DDI_"></span>TDR 设备驱动程序接口 (DDI)


为了适应此行为更改，显示微型端口驱动程序应实现这些函数：

-   [*DxgkDdiQueryDependentEngineGroup*](https://msdn.microsoft.com/library/windows/hardware/hh451407)
-   [*DxgkDdiQueryEngineStatus*](https://msdn.microsoft.com/library/windows/hardware/hh451411)
-   [*DxgkDdiResetEngine*](https://msdn.microsoft.com/library/windows/hardware/hh451418)

**请注意**  支持这些函数的驱动程序还必须支持零级同步[ *DxgkDdiCollectDbgInfo* ](https://msdn.microsoft.com/library/windows/hardware/ff559595)函数。 这是为了确保不会受到影响的调用是重置操作可以继续该零级微型端口。 请参阅备注的*DxgkDdiCollectDbgInfo*。

 

这些结构与相关联的新函数：

-   [**DXGK\_DRIVERCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff561062) (新**SupportPerEngineTDR**成员)
-   [**DXGK\_ENGINESTATUS**](https://msdn.microsoft.com/library/windows/hardware/hh464023)
-   [**DXGKARG\_QUERYDEPENDENTENGINEGROUP**](https://msdn.microsoft.com/library/windows/hardware/hh451294)
-   [**DXGKARG\_QUERYENGINESTATUS**](https://msdn.microsoft.com/library/windows/hardware/hh451299)
-   [**DXGKARG\_RESETENGINE**](https://msdn.microsoft.com/library/windows/hardware/hh451303)

显示微型端口驱动程序通过设置来指示对这些函数的支持[ **DXGK\_DRIVERCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff561062)。**SupportPerEngineTDR**成员，在这种情况下，它必须实现[ *DxgkDdiQueryDependentEngineGroup*](https://msdn.microsoft.com/library/windows/hardware/hh451407)， [ *DxgkDdiQueryEngineStatus*](https://msdn.microsoft.com/library/windows/hardware/hh451411)，并[ *DxgkDdiResetEngine* ](https://msdn.microsoft.com/library/windows/hardware/hh451418)函数。

## <a name="span-idtdrprocessdescriptionspanspan-idtdrprocessdescriptionspanspan-idtdrprocessdescriptionspantdr-process-description"></a><span id="TDR_process_description"></span><span id="tdr_process_description"></span><span id="TDR_PROCESS_DESCRIPTION"></span>TDR 进程说明


图形中常见的稳定性问题发生时系统处理的最终用户命令或操作时出现完全冻结或挂起。 通常在 GPU 正忙于处理密集型的图形操作，通常在游戏过程。 无屏幕更新发生，并且用户假定他们的系统已被冻结。 用户通常等待几秒钟，并按电源按钮，然后重新启动系统。

Windows Vista 和 Windows 7 尝试检测这些有问题的情况下的挂起和动态恢复响应式桌面。 不重新启动系统，但在大多数情况下屏幕闪烁如重绘。 但是，某些较旧的 Microsoft DirectX 应用程序呈现黑屏末尾的恢复，并且用户必须重新启动这些应用程序。 这些 GPU 挂起称为超时检测和恢复错误 (TDRs)。

该图显示了超时检测和恢复过程。 有关此过程的更多详细信息，请参阅[超时检测和恢复 (TDR)](timeout-detection-and-recovery.md)。

![超时检测和恢复 (tdr) 通过 wddm 进行 gpu](images/timeoutdetectionrecoverygpusthroughwddm.jpg)

GPU 命令已太长时间才能完成或挂起硬件时，会发生 TDRs。 TDRs 启用操作系统检测到不能响应式 UI。

## <a name="span-idnodesspanspan-idnodesspanspan-idnodesspannodes"></a><span id="Nodes"></span><span id="nodes"></span><span id="NODES"></span>节点


在上面的 TDR 函数中，使用*节点*是可以独立进行安排的单一物理适配器的多个部分之一。 例如，三维节点、 视频解码节点，和复制节点可以全部存在于同一个物理适配器，并且每个可以分配中的单独节点序号值[ **DXGKARG\_QUERYDEPENDENTENGINEGROUP**](https://msdn.microsoft.com/library/windows/hardware/hh451294).**NodeOrdinal**调用中的成员[ *DxgkDdiQueryDependentEngineGroup*](https://msdn.microsoft.com/library/windows/hardware/hh451407)。

通过显示微型端口驱动程序中报告的物理适配器中的节点数**NbAsymetricProcessingNodes**的成员[ **DXGK\_DRIVERCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff561062).**GpuEngineTopology**。

节点的序号值传入**NodeOrdinal**的成员[ **DXGKARG\_CREATECONTEXT** ](https://msdn.microsoft.com/library/windows/hardware/ff557567)结构时创建上下文。

## <a name="span-idenginesspanspan-idenginesspanspan-idenginesspanengines"></a><span id="Engines"></span><span id="engines"></span><span id="ENGINES"></span>引擎


在上面的 TDR 函数中，使用*引擎*是多个物理适配器 （或 Gpu） 之一的组合在一起作为一个逻辑适配器。 DirectX 图形内核子系统支持这种配置，但要求每个引擎必须具有相同的节点数。

例如，GPU 计划程序会考虑引擎 0 对应于物理适配器 0。 引擎 0 必须有引擎 1，对应于适配器 1 相同的节点数。

## <a name="span-idengineordinalvalueatcontextcreationspanspan-idengineordinalvalueatcontextcreationspanspan-idengineordinalvalueatcontextcreationspanengine-ordinal-value-at-context-creation"></a><span id="Engine_ordinal_value_at_context_creation"></span><span id="engine_ordinal_value_at_context_creation"></span><span id="ENGINE_ORDINAL_VALUE_AT_CONTEXT_CREATION"></span>引擎在上下文创建时的序号值


创建上下文后，设置引擎序号值对应的单个位**EngineAffinity**的成员[ **DXGKARG\_CREATECONTEXT** ](https://msdn.microsoft.com/library/windows/hardware/ff557567)结构。 **EngineOrdinal**这和计划程序相关的其他结构的成员是从零开始的索引。 值**EngineAffinity**为 1 &lt; &lt; **EngineOrdinal**，以及**EngineOrdinal**中的最高的位位置**EngineAffinity**。

## <a name="span-idpacketsunaffectedbyengineresetspanspan-idpacketsunaffectedbyengineresetspanspan-idpacketsunaffectedbyengineresetspanpackets-unaffected-by-engine-reset"></a><span id="Packets_unaffected_by_engine_reset"></span><span id="packets_unaffected_by_engine_reset"></span><span id="PACKETS_UNAFFECTED_BY_ENGINE_RESET"></span>数据包的引擎重置不会影响


GPU 计划程序可能要求驱动程序重新提交已太晚提交至引擎硬件队列引擎重置完成之前进行完全处理的数据包。 该驱动程序必须遵循以下准则来重新提交此类数据包：

-   *分页数据包*:GPU 计划程序将要求该驱动程序重新提交使用其原始隔离 Id，并按相同顺序的分页数据包，因为最初提交。 新的数据包被添加到的硬件队列之前，将重新提交任何此类数据包。
-   *呈现数据包*:GPU 计划程序将分配新的隔离 Id 的呈现器数据包，然后重新提交它们。

## <a name="span-idcallingsequencetoresetanenginespanspan-idcallingsequencetoresetanenginespanspan-idcallingsequencetoresetanenginespancalling-sequence-to-reset-an-engine"></a><span id="Calling_sequence_to_reset_an_engine"></span><span id="calling_sequence_to_reset_an_engine"></span><span id="CALLING_SEQUENCE_TO_RESET_AN_ENGINE"></span>若要重置引擎的调用序列


当[ *DxgkDdiResetEngine* ](https://msdn.microsoft.com/library/windows/hardware/hh451418)成功，GPU 计划程序可确保**LastAbortedFenceId**引擎重置调用返回的值对应到现有隔离 ID 的硬件队列中或在 GPU 上的最后一个已完成的隔离 ID。 后一种情况可能发生时的硬件队列清空后 GPU 超时检测到，但引擎重置回调之前进行调用。

在 GPU 上的最后一个已完成的隔离 ID 值必须维护驱动程序在任何时候因为还需要设置**DmaPreempted**。**LastCompletedFenceId**的成员[ **DXGKARGCB\_通知\_中断\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff557538)抢占中断通知结构。 应仅在这些情况下高级的最后一个已完成的隔离 ID:

-   完成数据包时 （不预先清空），最后一个已完成的隔离 ID 应设置为已完成数据包的隔离 ID。
-   当[ *DxgkDdiResetEngine* ](https://msdn.microsoft.com/library/windows/hardware/hh451418)成功，应将 ID 设置为值的最后一个已完成的 fence **LastCompletedFenceId**引擎返回的成员重置调用。
-   适配器范围重置，最后一个已完成的 fence ID 的所有节点上应将前移到最后一个提交在重置时隔离 ID。

下面是成功引擎重置，按时间顺序由 GPU 计划程序所示：

1.  颁发的抢占尝试。
2.  GPU 超时检测到。
3.  GPU 计划程序，最后一个提交和已完成隔离 Id 的快照，并忽略来自超时引擎的中断。 这是一个原子操作级别的设备的中断。
4.  如果不有任何数据包的硬件队列中在此时，退出。 如果数据包已完成在步骤 2 和 3 之间的时间窗口中，则可能发生此问题。
5.  所有排队的 Dpc 将被清除。
6.  准备引擎重置。
7.  调用[ *DxgkDdiResetEngine*](https://msdn.microsoft.com/library/windows/hardware/hh451418)。
8.  如果**LastAbortedFenceId**成员是早于最后一个已完成隔离 ID 或大于最后一个提交的隔离 ID，DirectX 图形内核子系统会导致系统出现 bugcheck 发生。 在崩溃转储文件中，记录该错误的消息**检测错误 0x119**，其中包含以下四个参数：
    -   0xA，这意味着该驱动程序报告了无效的中止的隔离 ID
    -   **LastAbortedFenceId**驱动程序返回值
    -   最后一个已完成的隔离 ID
    -   内部操作系统参数

9.  如果**LastAbortedFenceId**值是否有效，继续执行引擎重置恢复，如下所示。 如果分页数据包受引擎重置，则 GPU 计划程序遵循的引擎适配器范围重置重置。 拥有分配由该数据包引用的所有设备都将都置于错误状态以及。 但是，系统设备本身未置于错误状态，并且重置完成后恢复执行。

## <a name="span-idspecialcasesspanspan-idspecialcasesspanspan-idspecialcasesspanspecial-cases"></a><span id="Special_cases"></span><span id="special_cases"></span><span id="SPECIAL_CASES"></span>特殊情况


步骤 3 和步骤 7 上面所述之间在 GPU 上完成数据包时，可能发生特殊情况。 在这种情况下， **LastAbortedFenceId**从驱动程序的角度来看的硬件队列中没有数据包是否应设置为已完成的最后一个数据包的隔离 ID 驱动程序。 从计划程序的角度来看，它将出现此类数据包已中止，并且相应的设备将放入错误状态，即使最终完成数据包。

如果驱动程序不能执行重置操作因为硬件处于无效状态，或者由于硬件是不能进行的重置节点，该驱动程序应返回了失败状态代码。 如果 GPU 计划程序接收失败状态代码，它将执行适配器范围重置和重启操作以下[TDR 行为](timeout-detection-and-recovery.md)Windows 8 之前。

即使驱动程序已选择加入的 Windows 8 TDR 行为，也 GPU 计划程序请求重置和重启的整个逻辑适配器时将会用例。 因此，驱动程序必须还要实现[ *DxgkDdiResetFromTimeout* ](https://msdn.microsoft.com/library/windows/hardware/ff559815)并[ *DxgkDdiRestartFromTimeout* ](https://msdn.microsoft.com/library/windows/hardware/ff559820)函数，并它们的语义仍与 Windows 8 之前相同。 当尝试重置使用的物理适配器[ *DxgkDdiResetEngine* ](https://msdn.microsoft.com/library/windows/hardware/hh451418)引出的逻辑的适配器，重置 **！ 分析**Windows 调试器的命令显示**TdrReason** TDR 恢复上下文的值设置为一个新的值**TdrEngineTimeoutPromotedToAdapterReset** = 9。

## <a name="span-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


有关实现此功能时，必须满足硬件设备要求的信息，请参阅相关[WHCK 文档](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)上**Device.Graphics...TDRResiliency**。

请参阅[WDDM 1.2 功能](wddm-v1-2-features.md)评审的 Windows 8 一起添加的功能。

 

 





