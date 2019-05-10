---
title: 设备电源管理参考
description: 介绍驱动程序可用来将其设备硬件划分为多个逻辑组件，以启用细化的电源管理的 DDIs
keywords:
- AcceptDeviceNotification
ms.date: 12/17/2018
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 25ca4de5d7adac39596f7f5cd5fef1df5b04ea56
ms.sourcegitcommit: 944535d8e00393531f6b265317a64da3567e4f2c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65106377"
---
# <a name="device-power-management-reference"></a>设备电源管理参考

驱动程序可以将其设备硬件划分为多个逻辑组件，以启用细化的电源管理。 组件具有一组可以独立于其他组件在同一设备的电源状态管理的电源状态。 在 F0 状态下，该组件是完全打开的。 该组件可能支持其他、 低功耗状态 F1，F2，依次类推。

设备的电源策略所有者通常是设备的功能驱动程序。 若要启用组件级别电源管理，此驱动程序注册该设备[电源管理框架 (PoFx)](overview-of-the-power-management-framework.md)。 注册设备后，驱动程序假定组件时主动使用和组件处于空闲状态时通知 PoFx 的责任。 PoFx 使智能的空闲状态选择基于组件活动、 延迟偏差匹配、 预期空闲持续时间和唤醒要求有关的信息的设备。 通过在组件级别的控制电源使用情况，PoFx 可以减少电源需求，同时还能保留系统响应能力。 有关详细信息，请参阅[组件级别电源管理](component-level-power-management.md)。

## <a name="device-power-management-routines"></a>设备电源管理例程

这些例程被实现的电源管理框架 (PoFx) 以启用设备电源管理。 为设备的电源策略所有者 (PPO) 的驱动程序会调用这些例程。 通常情况下，设备功能驱动程序是此设备 PPO。

|主题|描述|
|----|----|
|[**PoFxActivateComponent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxactivatecomponent)|**PoFxActivateComponent**例程递增指定组件上的激活引用计数。|
|[PoFxCompleteDevicePowerNotRequired](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxcompletedevicepowernotrequired)|**PoFxCompleteDevicePowerNotRequired**例程通知电源管理框架 (PoFx) 的调用的驱动程序已完成的驱动程序的调用及其响应[ *DevicePowerNotRequiredCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_device_power_not_required_callback)回调例程。|
|[**PoFxCompleteIdleCondition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxcompleteidlecondition)|**PoFxCompleteIdleCondition**例程通知电源管理框架 (PoFx) 指定的组件已完成挂起的更改空闲条件。|
|[**PoFxCompleteIdleState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxcompleteidlestate)|PoFxCompleteIdleState 例程通知电源管理框架 (PoFx) 指定的组件已完成的 Fx 状态挂起的更改。|
|[**PoFxIdleComponent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxidlecomponent)|**PoFxIdleComponent**例程递减激活引用计数在指定的组件。|
|[**PoFxIssueComponentPerfStateChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxissuecomponentperfstatechange)|**PoFxIssueComponentPerfStateChange**例程提交请求以将设备组件放在特定的性能状态。|
|[**PoFxIssueComponentPerfStateChangeMultiple**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxissuecomponentperfstatechangemultiple)|**PoFxIssueComponentPerfStateChangeMultiple**例程提交请求以更改多个性能状态中的性能状态的设备组件同时设置。|
|[**PoFxNotifySurprisePowerOn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxnotifysurprisepoweron)|**PoFxNotifySurprisePowerOn**例程通知副作用是提供一些其他设备的电源开启设备电源管理框架 (PoFx)。|
|[**PoFxPowerControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxpowercontrol)|**PoFxPowerControl**例程将电源控制请求发送到电源管理框架 (PoFx)。|
|[**PoFxQueryCurrentComponentPerfState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxpowercontrol)|**PoFxQueryCurrentComponentPerfState**例程检索组件的性能状态组中的活动的性能状态。|
|[**PoFxRegisterComponentPerfStates**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxregistercomponentperfstates)|**PoFxRegisterComponentPerfStates**例程的电源管理框架 (PoFx) 中注册设备组件的性能状态管理。|
|[**PoFxRegisterDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxregisterdevice)|**PoFxRegisterDevice**例程与电源管理框架 (PoFx) 中注册的设备。|
|[**PoFxReportDevicePoweredOn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxreportdevicepoweredon)|**PoFxReportDevicePoweredOn**例程通知电源管理框架 (PoFx) 设备完成请求的转换到 D0 （完全启用） 电源状态。|
|[**PoFxSetComponentLatency**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxsetcomponentlatency)|**PoFxSetComponentLatency**例程从空闲条件转换为指定的组件中的活动条件中指定可以容忍的最大延迟。|
|[**PoFxSetComponentResidency**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxsetcomponentresidency)|**PoFxSetComponentResidency**例程设置多长时间，组件就可能保持空闲状态的组件将进入空闲状态的条件后的估计的时间。|
|[**PoFxSetComponentWake**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxsetcomponentwake)|**PoFxSetComponentWake**例程指示驱动程序是否而要唤醒组件将进入空闲条件时的指定的组件。|
|[**PoFxSetDeviceIdleTimeout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxsetdeviceidletimeout)|**PoFxSetDeviceIdleTimeout**例程指定最小时间间隔，从电源管理框架 (PoFx) 时调用的驱动程序到设备的最后一个组件时输入的空闲条件[ *DevicePowerNotRequiredCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_device_power_not_required_callback)回调例程。|
|[**PoFxStartDevicePowerManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxstartdevicepowermanagement)|**PoFxStartDevicePowerManagement**例程完成具有电源管理框架 (PoFx) 的设备的注册和启动设备电源管理。|
|[**PoFxUnregisterDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxunregisterdevice)|**PoFxUnregisterDevice**例程从电源管理框架 (PoFx) 删除的设备的注册。|

## <a name="device-power-management-callbacks"></a>设备电源管理回调

电源管理框架 (PoFx) 需要这些回调例程以启用设备电源管理。 为设备的电源策略所有者的驱动程序实现这些回调例程。 PoFx 调用这些例程来查询和在设备中配置组件的电源状态。

|主题|描述|
|----|----|
|[ComponentActiveConditionCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_active_condition_callback)|*ComponentActiveConditionCallback*回调例程会通知驱动程序指定的组件已完成从空闲条件转换到活动的条件。|
|[ComponentIdleConditionCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_idle_condition_callback)|*ComponentIdleConditionCallback*回调例程通知驱动程序指定的组件完成的活动条件从转换到空闲条件。|
|[ComponentIdleStateCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_idle_state_callback)|*ComponentIdleStateCallback*回调例程通知挂起的指定组件的 Fx 电源状态更改的驱动程序。|
|[ComponentPerfStateCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_perf_state_callback)|*ComponentPerfStateCallback*回调例程会通知驱动程序组件的性能状态更改其请求已完成。|
|[DevicePowerNotRequiredCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_device_power_not_required_callback)|*DevicePowerNotRequiredCallback*回调例程会通知的设备驱动程序设备不需要保留在 D0 电源状态。|
|[DevicePowerRequiredCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_device_power_required_callback)|*DevicePowerRequiredCallback*回调例程通知的设备必须输入并保留在 D0 电源状态的设备驱动程序。|
|[PowerControlCallback](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_power_control_callback)|*PowerControlCallback*回调例程执行请求的电源管理框架 (PoFx) 的电源管理操作。|

## <a name="device-power-management-structures"></a>设备电源管理结构

电源管理框架 (PoFx) 定义这些结构以支持设备电源管理。

|主题|描述|
|----|----|
|[PO_FX_COMPONENT_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_po_fx_component_v1)   [PO_FX_COMPONENT_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_po_fx_component_v2)|**PO_FX_COMPONENT**结构描述的设备中的组件的电源状态属性。|
|[PO_FX_COMPONENT_IDLE_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_po_fx_component_idle_state)|**PO_FX_COMPONENT_IDLE_STATE**结构设备中指定属性的组件的 Fx 电源状态。|
|[PO_FX_COMPONENT_PERF_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_po_fx_component_perf_info)|**PO_FX_COMPONENT_PERF_INFO**结构描述的设备中的单个组件的性能状态的所有集。|
|[PO_FX_COMPONENT_PERF_SET](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_po_fx_component_perf_set)|**PO_FX_COMPONENT_PERF_SET**结构表示一组设备中的单个组件的性能状态。|
|[PO_FX_DEVICE_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_po_fx_device_v1)   [PO_FX_DEVICE_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_po_fx_device_v2)   [PO_FX_DEVICE_V3](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-po_fx_device_v3)|**PO_FX_DEVICE**结构描述的电源管理框架 (PoFx) 的设备的 power 属性。|
|[PO_FX_PERF_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_po_fx_perf_state)|**PO_FX_PERF_STATE**结构表示设备内的单个组件的性能状态。|
|[PO_FX_PERF_STATE_CHANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_po_fx_perf_state_change)|**PO_FX_PERF_STATE_CHANGE**结构包含有关请求的调用的性能状态更改的信息[PoFxIssueComponentPerfStateChange](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxissuecomponentperfstatechange)或[PoFxIssueComponentPerfStateChangeMultiple](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxissuecomponentperfstatechangemultiple)例程。

## <a name="device-power-management-enumerations"></a>设备电源管理枚举

电源管理框架 (PoFx) 定义这些枚举以支持设备电源管理。

|主题|描述|
|----|----|
|[PO_FX_PERF_STATE_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_po_fx_perf_state_type)|**PO_FX_PERF_STATE_TYPE**枚举包含的描述中的性能状态的类型的值[PO_FX_COMPONENT_PERF_SET](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_po_fx_component_perf_set)。|
|[PO_FX_PERF_STATE_UNIT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_po_fx_perf_state_unit)|**PO_FX_PERF_STATE_UNIT**枚举包含的值，用于描述由性能状态控制的单位类型[PO_FX_COMPONENT_PERF_SET](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_po_fx_component_perf_set)。

## <a name="device-power-management-constants"></a>设备电源管理常量

### <a name="pofxflagxxx-flag-bits"></a>PO_FX_FLAG_XXX 标志位

**PO_FX_FLAG_XXX**常量是标志位，指示是否同步或异步执行请求以更改组件的条件。

```c++
#define PO_FX_FLAG_BLOCKING   0x1
#define PO_FX_FLAG_ASYNC_ONLY 0x2
```

#### <a name="pofxflagxxx-constants"></a>PO_FX_FLAG_XXX 常量

|Constant|描述|
|----|----|
|PO_FX_FLAG_BLOCKING|对更改的条件执行同步。 如果设置此标志，请求条件更改该例程不会控制返回给调用的驱动程序直到组件硬件完成转换到新的条件。 可以使用此标志，仅当调用方在 IRQL 运行 < DISPATCH_LEVEL。|
|PO_FX_FLAG_ASYNC_ONLY|将完全异步更改的条件。 如果设置此标志，是从称为请求条件更改该例程的线程以外的线程调用调用驱动程序的回调例程。 因此，始终请求条件更改该例程以异步方式返回而不等待要完成的回调。|

#### <a name="pofxflagxxx-remarks"></a>PO_FX_FLAG_XXX 备注

下面的例程的标志参数可设置为**PO_FX_FLAG_XXX**常量：

- [PoFxActivateComponent](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxactivatecomponent)
- [PoFxIdleComponent](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxidlecomponent)
- [PoFxIssueComponentPerfStateChange](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxissuecomponentperfstatechange)
- [PoFxIssueComponentPerfStateChangeMultiple](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxissuecomponentperfstatechangemultiple)

**PO_FX_FLAG_BLOCKING**并**PO_FX_FLAG_ASYNC_ONLY**标志位是互相排斥。 调用方可以在 Flags 参数，但不是两个标志位设置的一个或另一个标志位。

#### <a name="pofxflagxxx-requirements"></a>PO_FX_FLAG_XXX 要求

|Version|Header|
|----|----|
|支持从 Windows 8 开始。|Wdm.h|

### <a name="pofxflagperfxxx-flag-bits"></a>PO_FX_FLAG_PERF_XXX 标志位

**PO_FX_FLAG_PERF_XXX**常量是定义如何电源管理框架 (PoFx) 管理的设备组件的性能状态的标志位。

```c++
#define PO_FX_FLAG_PERF_PEP_OPTIONAL   0x1
#define PO_FX_FLAG_PERF_QUERY_ON_F0 0x2
#define PO_FX_FLAG_PERF_QUERY_ON_ALL_IDLE_STATES 0x4
```

|Constant|ReplTest1|描述|
|----|----|----|
|**PO_FX_FLAG_PERF_PEP_OPTIONAL**|1 (0x1)|指示该驱动程序可以从平台扩展插件 (PEP) 更改而无需协助的性能状态或，驱动程序注册到性能状态 PoFx 仅用于日志记录。 如果设置此标志， [PoFxRegisterComponentPerfStates](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxregistercomponentperfstates)调用将仍成功 PEP 不支持组件的性能状态。|
|**PO_FX_FLAG_PERF_QUERY_ON_F0**|2 (0x2)|对于某些设备，PEP 可能需要为性能状态设置为组件为某些性能状态的地方 (称为*名义上的性能状态*) 时，其空闲组件。 如果组件包含名义上的性能状态，用例 PoFx 查询以确定当前的性能状态时该组件将转换为 F0 PEP，驱动程序设置此标志。|
|**PO_FX_FLAG_PERF_QUERY_ON_ALL_IDLE_STATES**|4 (0x4)|对于某些设备，PEP 可能需要性能状态设置为组件为某些性能状态的位置 (称为*名义上的性能状态*) 时它将转换空闲状态之间的组件。 如果此组件包含名义上的性能状态，用例 PoFx 查询 PEP 来确定当前性能状态组件空闲状态之间转换时，驱动程序设置此标志。|

#### <a name="pofxflagperfxxx-remarks"></a>PO_FX_FLAG_PERF_XXX 备注

Flags 参数到[PoFxRegisterComponentPerfStates](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxregistercomponentperfstates)例程可以设置为**PO_FX_FLAG_PERF_XXX**常量。

#### <a name="pofxflagperfxxx-requirements"></a>PO_FX_FLAG_PERF_XXX 要求

|要求|Version|
|----|----|
|支持从 Windows 10 开始。|Wdm.h|
