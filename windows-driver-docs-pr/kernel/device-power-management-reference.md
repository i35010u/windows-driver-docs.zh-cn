---
title: 设备电源管理参考
description: 介绍驱动程序可用于将设备硬件划分为多个逻辑组件以实现精细电源管理的 DDIs
keywords:
- AcceptDeviceNotification
ms.date: 12/17/2018
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 309070d60180569bbccecc1d805c3a96da6827d0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838746"
---
# <a name="device-power-management-reference"></a>设备电源管理参考

驱动程序可以将设备硬件划分为多个逻辑组件，以实现精细的电源管理。 组件具有一组电源状态，可独立于同一设备中其他组件的电源状态进行管理。 在 F0 状态下，组件已完全打开。 组件可能支持其他低功耗状态 F1、F2 等。

设备的电源策略所有者通常是设备的功能驱动程序。 若要启用组件级电源管理，该驱动程序会将设备注册到[电源管理框架（PoFx）](overview-of-the-power-management-framework.md)。 通过注册设备，驱动程序假定在某个组件处于活动状态且组件处于空闲状态时，通知 PoFx 的责任。 PoFx 根据组件活动、延迟容差、预期空闲持续时间和唤醒要求的相关信息，为设备提供智能空闲状态选择。 通过在组件级控制电源使用情况，PoFx 可以降低电源要求，同时保留系统的响应能力。 有关详细信息，请参阅[组件级电源管理](component-level-power-management.md)。

## <a name="device-power-management-routines"></a>设备电源管理例程

这些例程由电源管理框架（PoFx）实现以启用设备电源管理。 这些例程由作为设备的电源策略所有者（PPO）的驱动程序调用。 通常，设备的函数驱动程序是此设备的 PPO。

|主题|描述|
|----|----|
|[**PoFxActivateComponent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxactivatecomponent)|**PoFxActivateComponent**例程会递增指定组件上的激活引用计数。|
|[PoFxCompleteDevicePowerNotRequired](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxcompletedevicepowernotrequired)|**PoFxCompleteDevicePowerNotRequired**例程通知电源管理框架（PoFx）调用驱动程序已完成对驱动程序的[*DevicePowerNotRequiredCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_device_power_not_required_callback)回调例程的调用的响应。|
|[**PoFxCompleteIdleCondition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxcompleteidlecondition)|**PoFxCompleteIdleCondition**例程通知电源管理框架（PoFx）指定的组件已完成对空闲状态的挂起更改。|
|[**PoFxCompleteIdleState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxcompleteidlestate)|PoFxCompleteIdleState 例程通知电源管理框架（PoFx）指定的组件已完成到 Fx 状态的挂起更改。|
|[**PoFxIdleComponent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxidlecomponent)|**PoFxIdleComponent**例程将减少指定组件上的激活引用计数。|
|[**PoFxIssueComponentPerfStateChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxissuecomponentperfstatechange)|**PoFxIssueComponentPerfStateChange**例程提交请求以将设备组件置于特定的性能状态。|
|[**PoFxIssueComponentPerfStateChangeMultiple**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxissuecomponentperfstatechangemultiple)|**PoFxIssueComponentPerfStateChangeMultiple**例程提交一个请求，以同时为设备组件更改多个性能状态集中的性能状态。|
|[**PoFxNotifySurprisePowerOn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxnotifysurprisepoweron)|**PoFxNotifySurprisePowerOn**例程通知电源管理框架（PoFx）已打开设备，作为为某个其他设备提供电源的副作用。|
|[**PoFxPowerControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxpowercontrol)|**PoFxPowerControl**例程将电源控制请求发送到电源管理框架（PoFx）。|
|[**PoFxQueryCurrentComponentPerfState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxpowercontrol)|**PoFxQueryCurrentComponentPerfState**例程检索组件的性能状态集中的活动性能状态。|
|[**PoFxRegisterComponentPerfStates**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxregistercomponentperfstates)|**PoFxRegisterComponentPerfStates**例程通过电源管理框架（PoFx）注册用于性能状态管理的设备组件。|
|[**PoFxRegisterDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxregisterdevice)|**PoFxRegisterDevice**例程向电源管理框架（PoFx）注册设备。|
|[**PoFxReportDevicePoweredOn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxreportdevicepoweredon)|**PoFxReportDevicePoweredOn**例程通知电源管理框架（PoFx）设备已将请求转换为 D0 （完全打开）电源状态。|
|[**PoFxSetComponentLatency**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxsetcomponentlatency)|**PoFxSetComponentLatency**例程指定在从空闲条件转换到指定组件中的活动条件时可容忍的最大延迟。|
|[**PoFxSetComponentResidency**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxsetcomponentresidency)|**PoFxSetComponentResidency**例程设置组件进入空闲状态后，组件可能保持空闲状态的估计时间。|
|[**PoFxSetComponentWake**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxsetcomponentwake)|**PoFxSetComponentWake**例程指示当组件进入空闲状态时，驱动程序是否会将指定的组件带到指定组件的唤醒状态。|
|[**PoFxSetDeviceIdleTimeout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxsetdeviceidletimeout)|**PoFxSetDeviceIdleTimeout**例程指定当电源管理框架（PoFx）调用驱动程序的[*DevicePowerNotRequiredCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_device_power_not_required_callback)时，从设备的最后一个组件进入空闲状态的最小时间间隔。回调例程。|
|[**PoFxStartDevicePowerManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxstartdevicepowermanagement)|**PoFxStartDevicePowerManagement**例程使用电源管理框架（PoFx）完成设备注册，并启动设备电源管理。|
|[**PoFxUnregisterDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxunregisterdevice)|**PoFxUnregisterDevice**例程从电源管理框架（PoFx）中删除设备注册。|

## <a name="device-power-management-callbacks"></a>设备电源管理回调

这些回调例程是电源管理框架（PoFx）必需的，用于启用设备电源管理。 作为设备的电源策略所有者的驱动程序实现了这些回调例程。 PoFx 调用这些例程来查询和配置设备中组件的电源状态。

|主题|描述|
|----|----|
|[ComponentActiveConditionCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_active_condition_callback)|*ComponentActiveConditionCallback*回调例程通知驱动程序指定的组件已完成从空闲条件到活动状态的转换。|
|[ComponentIdleConditionCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_idle_condition_callback)|*ComponentIdleConditionCallback*回调例程通知驱动程序指定的组件已完成从活动条件到空闲状态的转换。|
|[ComponentIdleStateCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_idle_state_callback)|*ComponentIdleStateCallback*回调例程通知驱动程序对指定组件的 Fx 电源状态的挂起更改。|
|[ComponentPerfStateCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_perf_state_callback)|*ComponentPerfStateCallback*回调例程通知驱动程序其更改组件的性能状态的请求已完成。|
|[DevicePowerNotRequiredCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_device_power_not_required_callback)|*DevicePowerNotRequiredCallback*回调例程通知设备驱动程序，设备不需要保持 D0 电源状态。|
|[DevicePowerRequiredCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_device_power_required_callback)|*DevicePowerRequiredCallback*回调例程通知设备驱动程序，设备必须进入并保持 D0 电源状态。|
|[PowerControlCallback](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_power_control_callback)|*PowerControlCallback*回调例程执行电源管理框架（PoFx）请求的电源控制操作。|

## <a name="device-power-management-structures"></a>设备电源管理结构

电源管理框架（PoFx）定义了这些结构以支持设备电源管理。

|主题|描述|
|----|----|
|[PO_FX_COMPONENT_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_po_fx_component_v1)   [PO_FX_COMPONENT_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_po_fx_component_v2)|**PO_FX_COMPONENT**结构描述设备中组件的电源状态属性。|
|[PO_FX_COMPONENT_IDLE_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_po_fx_component_idle_state)|**PO_FX_COMPONENT_IDLE_STATE**结构指定设备中组件的 FX 电源状态的属性。|
|[PO_FX_COMPONENT_PERF_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_po_fx_component_perf_info)|**PO_FX_COMPONENT_PERF_INFO**结构描述设备中单个组件的所有性能状态集。|
|[PO_FX_COMPONENT_PERF_SET](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_po_fx_component_perf_set)|**PO_FX_COMPONENT_PERF_SET**结构表示设备中单个组件的一组性能状态。|
|[PO_FX_DEVICE_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_po_fx_device_v1)   [PO_FX_DEVICE_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_po_fx_device_v2)   [PO_FX_DEVICE_V3](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-po_fx_device_v3)|**PO_FX_DEVICE**结构描述了电源管理框架（PoFx）设备的电源特性。|
|[PO_FX_PERF_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_po_fx_perf_state)|**PO_FX_PERF_STATE**结构表示设备中单个组件的性能状态。|
|[PO_FX_PERF_STATE_CHANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_po_fx_perf_state_change)|**PO_FX_PERF_STATE_CHANGE**结构包含有关通过调用[PoFxIssueComponentPerfStateChange](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxissuecomponentperfstatechange)或[PoFxIssueComponentPerfStateChangeMultiple](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxissuecomponentperfstatechangemultiple)请求的性能状态更改的信息例程.

## <a name="device-power-management-enumerations"></a>设备电源管理枚举

电源管理框架（PoFx）定义这些枚举以支持设备电源管理。

|主题|描述|
|----|----|
|[PO_FX_PERF_STATE_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_po_fx_perf_state_type)|**PO_FX_PERF_STATE_TYPE**枚举包含一些值，这些值描述了[PO_FX_COMPONENT_PERF_SET](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_po_fx_component_perf_set)中的性能状态的类型。|
|[PO_FX_PERF_STATE_UNIT](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_po_fx_perf_state_unit)|**PO_FX_PERF_STATE_UNIT**枚举包含一些值，这些值描述由[PO_FX_COMPONENT_PERF_SET](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_po_fx_component_perf_set)中的性能状态控制的单元类型。

## <a name="device-power-management-constants"></a>设备电源管理常量

### <a name="po_fx_flag_xxx-flag-bits"></a>PO_FX_FLAG_XXX 标志位

**PO_FX_FLAG_XXX**常量是标志位，指示更改组件条件的请求是同步执行还是异步执行。

```c++
#define PO_FX_FLAG_BLOCKING   0x1
#define PO_FX_FLAG_ASYNC_ONLY 0x2
```

#### <a name="po_fx_flag_xxx-constants"></a>PO_FX_FLAG_XXX 常量

|Constant|描述|
|----|----|
|PO_FX_FLAG_BLOCKING|使条件更改同步。 如果设置了此标志，则在组件硬件完成转换为新的条件之前，请求条件更改的例程不会将控制返回给调用驱动程序。 仅当调用方 < 在 DISPATCH_LEVEL 上运行时，才可以使用此标志。|
|PO_FX_FLAG_ASYNC_ONLY|将条件更改为完全异步。 如果设置了此标志，则调用驱动程序的回调例程将从线程（其中调用用于请求条件更改的例程）以外的线程调用。 因此，请求条件更改的例程始终以异步方式返回，而不等待回调完成。|

#### <a name="po_fx_flag_xxx-remarks"></a>PO_FX_FLAG_XXX 备注

可以将以下例程的 Flags 参数设置为**PO_FX_FLAG_XXX**常数：

- [PoFxActivateComponent](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxactivatecomponent)
- [PoFxIdleComponent](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxidlecomponent)
- [PoFxIssueComponentPerfStateChange](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxissuecomponentperfstatechange)
- [PoFxIssueComponentPerfStateChangeMultiple](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxissuecomponentperfstatechangemultiple)

**PO_FX_FLAG_BLOCKING**和**PO_FX_FLAG_ASYNC_ONLY**标志位互相排斥。 调用方可以在 Flags 参数中设置一个或另一个标志位，但不能同时设置这两个标志位。

#### <a name="po_fx_flag_xxx-requirements"></a>PO_FX_FLAG_XXX 要求

|版本|标头|
|----|----|
|从 Windows 8 开始支持。|Wdm。h|

### <a name="po_fx_flag_perf_xxx-flag-bits"></a>PO_FX_FLAG_PERF_XXX 标志位

**PO_FX_FLAG_PERF_XXX**常量是用于定义电源管理框架（PoFx）如何管理设备组件的性能状态的标志位。

```c++
#define PO_FX_FLAG_PERF_PEP_OPTIONAL   0x1
#define PO_FX_FLAG_PERF_QUERY_ON_F0 0x2
#define PO_FX_FLAG_PERF_QUERY_ON_ALL_IDLE_STATES 0x4
```

|Constant|Value|描述|
|----|----|----|
|**PO_FX_FLAG_PERF_PEP_OPTIONAL**|1（0x1）|指示驱动程序可以更改性能状态，而无需平台扩展插件（PEP）的帮助，或驱动程序正在为日志记录的 PoFx 注册性能状态。 如果设置了此标志，则如果 PEP 不支持组件的性能状态， [PoFxRegisterComponentPerfStates](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxregistercomponentperfstates)调用仍将成功。|
|**PO_FX_FLAG_PERF_QUERY_ON_F0**|2（0x2）|对于某些设备，PEP 可能需要在空闲组件时，将组件的性能状态设置为特定的性能状态（称为 "*标称性能状态*"）。 如果组件包含标称性能状态，则驱动程序将设置此标志，在这种情况下，PoFx 将在组件转换为 F0 时查询 PEP 来确定当前性能状态。|
|**PO_FX_FLAG_PERF_QUERY_ON_ALL_IDLE_STATES**|4（0x4）|对于某些设备，在将组件转换为空闲状态时，PEP 可能需要将组件的性能状态集设置为特定的性能状态（称为*标称性能状态*）。 驱动程序如果此组件包含标称性能状态，则会设置此标志，在这种情况下，PoFx 将在该组件在空闲状态之间转换时查询 PEP 来确定当前性能状态。|

#### <a name="po_fx_flag_perf_xxx-remarks"></a>PO_FX_FLAG_PERF_XXX 备注

[PoFxRegisterComponentPerfStates](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxregistercomponentperfstates)例程的 Flags 参数可以设置为**PO_FX_FLAG_PERF_XXX**常量。

#### <a name="po_fx_flag_perf_xxx-requirements"></a>PO_FX_FLAG_PERF_XXX 要求

|要求|版本|
|----|----|
|从 Windows 10 开始支持。|Wdm。h|
