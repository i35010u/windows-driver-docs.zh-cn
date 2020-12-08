---
title: 设备电源管理 (DPM) 通知
description: 每个设备电源管理 (的 DPM) 通知： PEP 的 AcceptDeviceNotification 回调例程收到的通知参数会附带指示通知类型的通知参数，以及指向包含指定通知类型信息的数据结构的数据参数。
keywords:
- AcceptDeviceNotification
ms.date: 01/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 25424b1727baae3a4833ceb1023c5605e5c3d9d1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825913"
---
# <a name="device-power-management-dpm-notifications"></a>设备电源管理 (DPM) 通知

每个设备电源管理 (的 DPM) 通知： PEP 的 AcceptDeviceNotification 回调例程收到的通知参数会附带指示通知类型的通知参数，以及指向包含指定通知类型信息的数据结构的数据参数。

在此调用中，通知参数设置为指示通知类型 PEP_DPM_XXX 常量值。 数据参数指向与此通知类型相关联的 PEP_XXX 结构类型。

|通知 ID|“值”|关联的结构|
|----|----|----|
|[PEP_DPM_PREPARE_DEVICE](#pep_dpm_prepare_device)|0x01|[PEP_PREPARE_DEVICE](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_prepare_device)|
|[PEP_DPM_ABANDON_DEVICE](#pep_dpm_abandon_device)|0x02|[PEP_ABANDON_DEVICE](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_abandon_device)|
|[PEP_DPM_REGISTER_DEVICE](#pep_dpm_register_device)|0x03|[PEP_REGISTER_DEVICE_V2](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_register_device_v2)|
|[PEP_DPM_UNREGISTER_DEVICE](#pep_dpm_unregister_device)|0x04|[PEP_UNREGISTER_DEVICE](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_unregister_device)|
|[PEP_DPM_DEVICE_POWER_STATE](#pep_dpm_device_power_state)|0x05|[PEP_DEVICE_POWER_STATE](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_device_power_state)|
|[PEP_DPM_COMPONENT_ACTIVE](#pep_dpm_component_active)|0x07|[PEP_COMPONENT_ACTIVE](/windows-hardware/drivers/ddi/pep_x/ns-pep_x-_pep_component_active)|
|[PEP_DPM_WORK](#pep_dpm_work)|0x0D|[PEP_WORK](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_work)|
|[PEP_DPM_POWER_CONTROL_REQUEST](#pep_dpm_power_control_request)|0x0E|[PEP_POWER_CONTROL_REQUEST](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_power_control_request)|
|[PEP_DPM_POWER_CONTROL_COMPLETE](#pep_dpm_power_control_complete)|0x0F|[PEP_POWER_CONTROL_COMPLETE](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_power_control_complete)|
|[PEP_DPM_SYSTEM_LATENCY_UPDATE](#pep_dpm_system_latency_update)|0x10|[PEP_SYSTEM_LATENCY](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_system_latency)|
|[PEP_DPM_DEVICE_STARTED](#pep_dpm_device_started)|0x12|[PEP_DEVICE_STARTED](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_device_started)|
|[PEP_DPM_NOTIFY_COMPONENT_IDLE_STATE](#pep_dpm_notify_component_idle_state)|0x13|[PEP_NOTIFY_COMPONENT_IDLE_STATE](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_notify_component_idle_state)|
|[PEP_DPM_REGISTER_DEBUGGER](#pep_dpm_register_debugger)|0x15|[PEP_REGISTER_DEBUGGER](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_register_debugger)|
|[PEP_DPM_LOW_POWER_EPOCH](#pep_dpm_low_power_epoch)|0x18|[PEP_LOW_POWER_EPOCH](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_low_power_epoch)|
|[PEP_DPM_REGISTER_CRASHDUMP_DEVICE](#pep_dpm_register_crashdump_device)|0x19|[PEP_REGISTER_CRASHDUMP_DEVICE](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_register_crashdump_device)|
|[PEP_DPM_DEVICE_IDLE_CONSTRAINTS](#pep_dpm_device_idle_constraints)|0x1A|[PEP_DEVICE_PLATFORM_CONSTRAINTS](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_device_platform_constraints)|
|[PEP_DPM_COMPONENT_IDLE_CONSTRAINTS](#pep_dpm_component_idle_constraints)|0x1B|[PEP_COMPONENT_PLATFORM_CONSTRAINTS](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_component_platform_constraints)|
|[PEP_DPM_QUERY_COMPONENT_PERF_CAPABILITIES](#pep_dpm_query_component_perf_capabilities)|0x1C|[PEP_QUERY_COMPONENT_PERF_CAPABILITIES](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_query_component_perf_capabilities)|
|[PEP_DPM_QUERY_COMPONENT_PERF_SET](#pep_dpm_query_component_perf_set)|0x1D|[PEP_QUERY_COMPONENT_PERF_SET](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_query_component_perf_set)|
|[PEP_DPM_QUERY_COMPONENT_PERF_SET_NAME](#pep_dpm_query_component_perf_set_name)|0x1E|[PEP_QUERY_COMPONENT_PERF_SET_NAME](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_query_component_perf_set_name)|
|[PEP_DPM_QUERY_COMPONENT_PERF_STATES](#pep_dpm_query_component_perf_states)|0x1F|[PEP_QUERY_COMPONENT_PERF_STATES](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_query_component_perf_states)|
|[PEP_DPM_REGISTER_COMPONENT_PERF_STATES](#pep_dpm_register_component_perf_states)|0x20|[PEP_REGISTER_COMPONENT_PERF_STATES](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_register_component_perf_states)|
|[PEP_DPM_REQUEST_COMPONENT_PERF_STATE](#pep_dpm_request_component_perf_state)|0x21|[PEP_REQUEST_COMPONENT_PERF_STATE](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_request_component_perf_state)|
|[PEP_DPM_QUERY_CURRENT_COMPONENT_PERF_STATE](#pep_dpm_query_current_component_perf_state)|0x22|[PEP_QUERY_CURRENT_COMPONENT_PERF_STATE](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_query_current_component_perf_state)|
|[PEP_DPM_QUERY_DEBUGGER_TRANSITION_REQUIREMENTS](#pep_dpm_query_debugger_transition_requirements)|0x23|[PEP_DEBUGGER_TRANSITION_REQUIREMENTS](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_debugger_transition_requirements)|
|[PEP_DPM_QUERY_SOC_SUBSYSTEM_COUNT](#pep_dpm_query_soc_subsystem_count)|0x24|[PEP_QUERY_SOC_SUBSYSTEM_COUNT](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_query_soc_subsystem_count)|
|[PEP_DPM_QUERY_SOC_SUBSYSTEM](#pep_dpm_query_soc_subsystem)|0x25|[PEP_QUERY_SOC_SUBSYSTEM](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_query_soc_subsystem)|
|[PEP_DPM_RESET_SOC_SUBSYSTEM_ACCOUNTING](#pep_dpm_reset_soc_subsystem_accounting)|0x26|[PEP_RESET_SOC_SUBSYSTEM_ACCOUNTING](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_reset_soc_subsystem_accounting)|
|[PEP_DPM_QUERY_SOC_SUBSYSTEM_BLOCKING_TIME](#pep_dpm_query_soc_subsystem_blocking_time)|0x27|[PEP_QUERY_SOC_SUBSYSTEM_BLOCKING_TIME](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_query_soc_subsystem_blocking_time)|
|[PEP_DPM_QUERY_SOC_SUBSYSTEM_METADATA](#pep_dpm_query_soc_subsystem_metadata)|0x28|[PEP_QUERY_SOC_SUBSYSTEM_METADATA](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_query_soc_subsystem_metadata)|

## <a name="notification-ids"></a>通知 Id

AcceptDeviceNotification 回调例程使用以下 DPM 通知 Id。

### <a name="pep_dpm_prepare_device"></a>PEP_DPM_PREPARE_DEVICE

#### <a name="notification-pep_dpm_prepare_device"></a>通知 (PEP_DPM_PREPARE_DEVICE) 

PEP_DPM_PREPARE_DEVICE 的值。

#### <a name="data-pep_dpm_prepare_device"></a>数据 (PEP_DPM_PREPARE_DEVICE) 

指向 [PEP_PREPARE_DEVICE](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_prepare_device) 结构的指针。 告知拥有指定设备的 PEP 将设备配置为在 D0 (工作) 设备电源状态下运行。

在设备的驱动程序堆栈第一次启动后，Windows 电源管理框架 (PoFx) 将此通知发送到 PEP。 此通知允许 PEP 打开操作设备所需的任何外部电源或时钟资源。

为了发送 PEP_DPM_PREPARE_DEVICE 通知，操作系统将调用 PEP 的 AcceptDeviceNotification 回调例程。 在此调用中，通知参数值为 PEP_DPM_PREPARE_DEVICE，数据参数指向 PEP_PREPARE_DEVICE 结构。 在输入时，此结构的 DeviceId 成员是唯一标识设备的设备标识字符串。 在返回之前，PEP 将此结构的 DeviceAccepted 成员设置为 TRUE，以声明设备的所有权，或设置为 FALSE 以指示它不拥有设备。

拥有设备的电源管理的 PEP 负责管理设备外部以及操作设备所需的电源和时钟资源。 此 PEP 使时钟信号和设备能够响应 PEP_DPM_PREPARE_DEVICE 通知，并从设备中删除时钟信号和电源，以响应 PEP_DPM_ABANDON_DEVICE 通知。

下表显示了在此操作系统将 PEP_DPM_PREPARE_DEVICE 通知发送到 PEP 时生效的前提条件，以及在 PEP 为其拥有的设备处理此通知后必须生效的后置条件。

|Preconditions|Postconditions|
|----|----|
|设备可以处于任何电源状态。|如果 PEP 宣称设备的所有权，则设备及其所有组件必须处于打开状态，并且设备的时钟必须无选通。</br>当电源管理器尝试查找这些设备的 PEP 所有者时，PEP 可以接收多个设备的 PEP_DPM_PREPARE_DEVICE 通知。 对于 PEP 不拥有的所有设备，PEP 应将 PEP_PREPARE_DEVICE 结构的 DeviceAccepted 成员设置为 FALSE。

不会为核心设备发送 PEP_DPM_PREPARE_DEVICE 通知。

对于 PEP_DPM_PREPARE_DEVICE 通知，AcceptDeviceNotification 例程始终调用 IRQL = PASSIVE_LEVEL。

### <a name="pep_dpm_abandon_device"></a>PEP_DPM_ABANDON_DEVICE

#### <a name="notification-pep_dpm_abandon_device"></a>通知 (PEP_DPM_ABANDON_DEVICE) 

PEP_DPM_ABANDON_DEVICE 的值。

#### <a name="data-pep_dpm_abandon_device"></a>数据 (PEP_DPM_ABANDON_DEVICE) 

指向 [PEP_ABANDON_DEVICE](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_abandon_device) 结构的指针。
告诉 PEP，操作系统不再使用指定的设备。

当操作系统删除设备的驱动程序堆栈后，Windows 电源管理框架 (PoFx) 会将此通知发送到 PEP。 此通知允许 PEP 关闭用于操作设备的所有外部电源或时钟资源，并从将来的决策过程中删除此设备。 如果以后必须重新启动设备，PEP 将首先收到 PEP_DPM_PREPARE_DEVICE 通知。

为了发送 PEP_DPM_ABANDON_DEVICE 通知，操作系统将调用 PEP 的 AcceptDeviceNotification 回调例程。 在此调用中，通知参数值为 PEP_DPM_ABANDON_DEVICE，数据参数指向 PEP_ABANDON_DEVICE 结构。 在输入时，此结构的 DeviceId 成员是唯一标识设备的设备标识字符串。 在返回之前，PEP 将此结构的 DeviceAccepted 成员设置为 TRUE，以声明设备的所有权，或设置为 FALSE 以指示它不拥有设备。

拥有设备的电源管理的 PEP 负责管理设备外部以及操作设备所需的电源和时钟资源。

下表显示了在此操作系统将 PEP_DPM_ABANDON_DEVICE 通知发送到 PEP 时生效的前提条件，以及在 PEP 为其拥有的设备处理此通知后必须生效的后置条件。

|Preconditions|Postconditions|
|----|----|
|PEP 接收到设备的 PEP_DPM_PREPARE_DEVICE 通知，并已接受设备的所有权。</br>如果 PEP 接收到设备的 PEP_DPM_REGISTER_DEVICE 通知并接受设备注册，则它随后收到设备的 PEP_DPM_UNREGISTER_DEVICE 通知。|必须释放为响应 PEP_DPM_PREPARE_DEVICE 通知而分配的任何资源。</br>对于 PEP_DPM_PREPARE_DEVICE 通知，AcceptDeviceNotification 例程始终调用 IRQL = PASSIVE_LEVEL。|

### <a name="pep_dpm_register_device"></a>PEP_DPM_REGISTER_DEVICE

#### <a name="notification-pep_dpm_register_device"></a>通知 (PEP_DPM_REGISTER_DEVICE) 

PEP_DPM_REGISTER_DEVICE 的值。

#### <a name="data-pep_dpm_register_device"></a>数据 (PEP_DPM_REGISTER_DEVICE) 

指向 [PEP_REGISTER_DEVICE_V2](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_register_device_v2) 结构的指针。

告知 PEP：指定设备的驱动程序堆栈已向 Windows 电源管理框架注册 (PoFx) 。

当设备的驱动程序堆栈调用 PoFxRegisterDevice 例程来注册设备时，PoFx 将发送此通知。 此通知允许 PEP 将设备的注册信息复制到 PEP 的内部存储，供以后参考。

为了发送 PEP_DPM_REGISTER_DEVICE 通知，操作系统将调用 PEP 的 AcceptDeviceNotification 回调例程。 在此调用中，通知参数值为 PEP_DPM_REGISTER_DEVICE，Data 参数指向包含设备内核句柄和其他注册信息的 PEP_REGISTER_DEVICE_V2 结构。 在输入时，此结构的 DeviceId 成员是唯一标识设备的设备标识字符串。 在返回之前，PEP 将此结构的 DeviceAccepted 成员设置为 TRUE，以声明设备的所有权，或设置为 FALSE 以指示它不拥有设备。 有关此结构的其他成员的信息，请参阅 PEP_REGISTER_DEVICE_V2。

下表显示了在此操作系统将 PEP_DPM_REGISTER_DEVICE 通知发送到 PEP 时生效的前提条件，以及在 PEP 为其拥有的设备处理此通知后必须生效的后置条件。

|Preconditions|Postconditions|
|----|----|
|PEP 接收到其拥有的设备的 PEP_DPM_PREPARE_DEVICE 通知。|PEP 已准备好接收其他设备电源管理 (与此设备关联的 DPM) 通知。|

对于 PEP_DPM_REGISTER_DEVICE 通知，AcceptDeviceNotification 例程始终调用 IRQL = PASSIVE_LEVEL。

### <a name="pep_dpm_unregister_device"></a>PEP_DPM_UNREGISTER_DEVICE

#### <a name="notification-pep_dpm_unregister_device"></a>通知 (PEP_DPM_UNREGISTER_DEVICE) 

PEP_DPM_UNREGISTER_DEVICE 的值。

#### <a name="data-pep_dpm_unregister_device"></a>数据 (PEP_DPM_UNREGISTER_DEVICE) 

指向 [PEP_UNREGISTER_DEVICE](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_unregister_device) 结构的指针。

告知拥有指定设备的 PEP，设备的驱动程序堆栈已从 Windows 电源管理框架中撤销了其注册 (PoFx) 。

PoFx 将发送此通知，告知 PEP：在上一个 PEP_DPM_REGISTER_DEVICE 通知期间，PEP 为设备存储的所有注册信息都不再有效。 在响应中，PEP 可以清理此设备的电源管理使用的任何内部状态。

为了发送 PEP_DPM_UNREGISTER_DEVICE 通知，操作系统将调用 PEP 的 AcceptDeviceNotification 回调例程。 在此调用中，通知参数值为 PEP_DPM_UNREGISTER_DEVICE，数据参数指向 PEP_UNREGISTER_DEVICE 结构。 此结构包含 PEP 为响应先前 PEP_DPM_REGISTER_DEVICE 设备通知而创建的句柄。

下表显示了在此操作系统将 PEP_DPM_UNREGISTER_DEVICE 通知发送到 PEP 时生效的前提条件，以及在 PEP 为其拥有的设备处理此通知后必须生效的后置条件。

|Preconditions|Postconditions|
|----|----|
|如果 PEP 收到设备的 PEP_DPM_REGISTER_DEVICE 通知并接受设备注册，则为。</br>PEP 可以接收任何设备电源管理 (与此设备关联的 DPM) 通知。</br>PEP 可以报告与此设备关联的 "工作"。|除 PEP_DPM_ABANDON_DEVICE 外，PEP 不能再接收与此设备相关联 (DPM) 通知的任何设备电源管理。</br>PEP 无法报告与此设备关联的 "工作"。|

对于 PEP_DPM_UNREGISTER_DEVICE 通知，AcceptDeviceNotification 例程始终调用 IRQL = PASSIVE_LEVEL。

### <a name="pep_dpm_device_power_state"></a>PEP_DPM_DEVICE_POWER_STATE

#### <a name="notification-pep_dpm_device_power_state"></a>通知 (PEP_DPM_DEVICE_POWER_STATE) 

PEP_DPM_DEVICE_POWER_STATE 的值。

#### <a name="data-pep_dpm_device_power_state"></a>数据 (PEP_DPM_DEVICE_POWER_STATE) 

指向 [PEP_DEVICE_POWER_STATE](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_device_power_state) 结构的指针。

每次设备的驱动程序堆栈请求更改为新的 Dx 电源状态或以前请求的到 Dx 电源状态的转换时，都会发送到 PEP。

在 PEP 调用 RequestWorker 例程来请求工作项后，PoFx 将通过向 PEP 发送 PEP_DPM_DEVICE_POWER_STATE 通知来做出响应。 但是，在 (的资源（) 处理工作项所需的工作线程可用）之前，不会发送此通知。 通过这种方式，PoFx 保证在通知过程中，PEP 传递到 PoFx 的工作请求永远不会因资源不足而失败。

为了发送 PEP_DPM_DEVICE_POWER_STATE 通知，操作系统将调用 PEP 的 AcceptDeviceNotification 回调例程。 在此调用中，通知参数值为 PEP_DPM_DEVICE_POWER_STATE，数据参数指向 PEP_DEVICE_POWER_STATE 结构。 输入时，PEP 应假设此结构的内容未初始化。 为了处理此通知，PEP 应将 WorkInformation 成员设置为指向 PEP 分配的 PEP_WORK_INFORMATION 结构，该结构描述正在请求的工作。 此外，PEP 应将 PEP_WORK 结构的 NeedWork 成员设置为 TRUE，以确认 PEP 已处理 PEP_DEVICE_POWER_STATE 通知，并且 WorkInformation 成员指向有效的 PEP_WORK_INFORMATION 结构。 如果 PEP 无法处理通知或无法分配 PEP_WORK_INFORMATION 结构，则 PEP 应将 WorkInformation 成员设置为 NULL，并将 NeedWork 成员设置为 FALSE。

对于 PEP_DPM_DEVICE_POWER_STATE 通知，AcceptDeviceNotification 例程始终调用 IRQL = PASSIVE_LEVEL。

### <a name="pep_dpm_component_active"></a>PEP_DPM_COMPONENT_ACTIVE

#### <a name="notification-pep_dpm_component_active"></a>通知 (PEP_DPM_COMPONENT_ACTIVE) 

PEP_DPM_COMPONENT_ACTIVE 的值。

#### <a name="data-pep_dpm_component_active"></a>数据 (PEP_DPM_COMPONENT_ACTIVE) 

一个指向 [PEP_COMPONENT_ACTIVE](/windows-hardware/drivers/ddi/pep_x/ns-pep_x-_pep_component_active) 结构的指针，该结构标识组件，并指示此组件是转换为活动条件还是向空闲状态进行转换。

通知 PEP：组件需要从空闲条件转换为活动条件，反之亦然。

Windows 电源管理框架 (PoFx) 在将转换挂起到活动状态或进入空闲状态时，发送此通知。

若要发送 PEP_DPM_COMPONENT_ACTIVE 通知，PoFx 将调用 PEP 的 AcceptDeviceNotification 回调例程。 在此调用中，通知参数值为 PEP_DPM_COMPONENT_ACTIVE，数据参数指向 PEP_COMPONENT_ACTIVE 结构。

可访问的组件处于活动状态。 不可访问的组件处于空闲状态。 处于活动状态的组件始终处于 F0 组件电源状态。 该组件在进入空闲状态之前无法退出 F0。 处于空闲状态的组件可能处于 F0 或低能耗 Fx 状态。 组件的活动/空闲条件是驱动程序确定是否可访问组件的唯一可靠方法。 位于 F0，但也处于空闲状态的组件可能会切换为低功率 Fx 状态。

当活动组件准备好进入空闲状态时，转换将立即进行。 例如，在处理 PEP_DPM_COMPONENT_ACTIVE 通知的过程中，PEP 可能会请求从 F0 转换为组件的低功率 Fx 状态。

如果在 PEP_DPM_COMPONENT_ACTIVE 通知请求从空闲条件转换为活动条件时，组件处于低功耗 Fx 状态，则 PEP 必须先将组件切换到 F0，然后组件才能进入活动状态。 在从 PEP_DPM_COMPONENT_ACTIVE 通知的 AcceptDeviceNotification 回调返回后，PEP 可能需要完成为异步转换到活动条件而准备的组件。 将组件完全配置为在活动状态下操作后，PEP 必须调用 RequestWorker 例程，然后通过在 PEP_WORK_INFORMATION 结构中设置 WorkType = PepWorkActiveComplete 来处理生成的 PEP_DPM_WORK 通知。

如果 PEP 接收到 F0 中组件的 PEP_DPM_COMPONENT_ACTIVE 通知，并且已经完全配置为在活动状态下操作，则 PEP 可能能够同步处理此通知。 如果支持通知的 "快速路径" 处理，则此通知的 PEP_COMPONENT_ACTIVE 结构的 WorkInformation 成员包含指向 PEP_WORK_INFORMATION 结构的指针，并且 PEP 可以将此结构的 WorkType 成员设置为 PepWorkActiveComplete 以完成转换。 但是，如果 WorkInformation = NULL，则不能使用 "快速路径"，并且 PEP 必须通过调用 RequestWorker 异步完成转换，如前一段所述。

有关活动和空闲情况的详细信息，请参阅 [组件级电源管理](component-level-power-management.md)。

对于 PEP_DPM_COMPONENT_ACTIVE 通知，AcceptDeviceNotification 例程以 IRQL <= DISPATCH_LEVEL 调用。

### <a name="pep_dpm_work"></a>PEP_DPM_WORK

#### <a name="notification-pep_dpm_work"></a>通知 (PEP_DPM_WORK) 

PEP_DPM_WORK 的值。

#### <a name="data-pep_dpm_work"></a>数据 (PEP_DPM_WORK) 

指向 [PEP_WORK](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_work) 结构的指针。

每次 PEP 调用 RequestWorker 例程来请求 Windows 电源管理框架中的工作项时，都会发送到 PEP (PoFx) 。

在 PEP 调用 RequestWorker 例程来请求工作项后，PoFx 将通过向 PEP 发送 PEP_DPM_WORK 通知来做出响应。 但是，在 (的资源（) 处理工作项所需的工作线程可用）之前，不会发送此通知。 通过这种方式，PoFx 保证在通知过程中，PEP 传递到 PoFx 的工作请求永远不会因资源不足而失败。

为了发送 PEP_DPM_WORK 通知，操作系统将调用 PEP 的 AcceptDeviceNotification 回调例程。 在此调用中，通知参数值为 PEP_DPM_WORK，数据参数指向 PEP_WORK 结构。 输入时，PEP 应假设此结构的内容未初始化。 为了处理此通知，PEP 应将 WorkInformation 成员设置为指向 PEP 分配的 PEP_WORK_INFORMATION 结构，该结构描述正在请求的工作。 此外，PEP 应将 PEP_WORK 结构的 NeedWork 成员设置为 TRUE，以确认 PEP 已处理 PEP_DPM_WORK 通知，并且 WorkInformation 成员指向有效的 PEP_WORK_INFORMATION 结构。 如果 PEP 无法处理通知或无法分配 PEP_WORK_INFORMATION 结构，则 PEP 应将 WorkInformation 成员设置为 NULL，并将 NeedWork 成员设置为 FALSE。

对于 PEP_DPM_WORK 通知，AcceptDeviceNotification 例程始终调用 IRQL = PASSIVE_LEVEL。

### <a name="pep_dpm_power_control_request"></a>PEP_DPM_POWER_CONTROL_REQUEST

#### <a name="notification-pep_dpm_power_control_request"></a>通知 (PEP_DPM_POWER_CONTROL_REQUEST) 

PEP_DPM_POWER_CONTROL_REQUEST 的值。

#### <a name="data-pep_dpm_power_control_request"></a>数据 (PEP_DPM_POWER_CONTROL_REQUEST) 

指向 [PEP_POWER_CONTROL_REQUEST](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_power_control_request) 结构的指针。

通知 PEP 驱动程序已调用 PoFxPowerControl API，以将控制代码直接发送到 PEP。

当驱动程序调用 PoFxPowerControl API 将控制代码直接发送到 PEP 时，Windows 电源管理框架 (PoFx) 会将此通知发送到 PEP。 此情况下，通知数据指针指向 PEP_POWER_CONTROL_REQUEST 结构

Power control 请求及其语义在 PEP 编写器和设备类所有者之间定义。 通常，此类接口用于特定于设备类的通信，而不是在通用电源管理框架中捕获的。 例如，UART 控制器可能会将波特率信息传递给 PEP 来修改某些平台时钟导轨/分隔线，此类通信可能利用电源控制请求。

>!纪录在收到 PEP_DPM_DEVICE_STARTED 通知或 PEP_DPM_POWER_CONTROL_REQUEST 通知后，PEP 只能请求将控制代码发送到设备。

对于 PEP_DPM_POWER_CONTROL_REQUEST 通知，AcceptDeviceNotification 例程以 IRQL <= DISPATCH_LEVEL 调用。

### <a name="pep_dpm_power_control_complete"></a>PEP_DPM_POWER_CONTROL_COMPLETE

#### <a name="notification-pep_dpm_power_control_complete"></a>通知 (PEP_DPM_POWER_CONTROL_COMPLETE) 

PEP_DPM_POWER_CONTROL_COMPLETE 的值。

#### <a name="data-pep_dpm_power_control_complete"></a>数据 (PEP_DPM_POWER_CONTROL_COMPLETE) 

指向 [PEP_POWER_CONTROL_COMPLETE](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_power_control_complete) 结构的指针。

通知 PEP 驱动程序已完成由 PEP 颁发的 power control 请求

当驱动程序完成由 PEP 发出的电源控制请求时，Windows 电源管理框架 (PoFx) 会将此通知发送到 PEP。

>!纪录如果 PEP 未发出任何电源控制请求，则 PEP 可以忽略此通知。

对于 PEP_DPM_POWER_CONTROL_COMPLETE 通知，AcceptDeviceNotification 例程以 IRQL <= DISPATCH_LEVEL 调用。

### <a name="pep_dpm_system_latency_update"></a>PEP_DPM_SYSTEM_LATENCY_UPDATE

#### <a name="notification-pep_dpm_system_latency_update"></a>通知 (PEP_DPM_SYSTEM_LATENCY_UPDATE) 

PEP_DPM_SYSTEM_LATENCY_UPDATE 的值。

#### <a name="data-pep_dpm_system_latency_update"></a>数据 (PEP_DPM_SYSTEM_LATENCY_UPDATE) 

指向 [PEP_SYSTEM_LATENCY](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_system_latency) 结构的指针。

通知 PEP 操作系统已更新整个系统延迟容差。

Windows 电源管理框架 (PoFx) 在操作系统更新整体系统延迟容差时发送此通知。

在早期版本的 PoFx 中，PEP 使用此通知来进行处理器和平台空闲状态选择。 使用最新的 PEP 接口，选择过程由操作系统完全处理，因此此通知不再有用。 本文包含此内容是为了保持完整性，并且 PEP 应忽略它。

若要发送 PEP_DPM_SYSTEM_LATENCY_UPDATE 通知，PoFx 将调用 PEP 的 AcceptDeviceNotification 回调例程。 对于此通知，AcceptDeviceNotification 例程在 IRQL <= DISPATCH_LEVEL 中调用。

### <a name="pep_dpm_device_started"></a>PEP_DPM_DEVICE_STARTED

#### <a name="notification-pep_dpm_device_started"></a>通知 (PEP_DPM_DEVICE_STARTED) 

PEP_DPM_DEVICE_STARTED 的值。

#### <a name="data-pep_dpm_device_started"></a>数据 (PEP_DPM_DEVICE_STARTED) 

指向 [PEP_DEVICE_STARTED](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_device_started) 结构的指针。

通知 PEP 设备已启动，使其可用于接收电源控制事务。

在两个步骤的过程中，设备堆栈向操作系统注册运行时电源管理。 驱动程序首先调用 PoFxRegisterDevice 以提供有关组件数量、其空闲状态和相应属性的信息。 为了响应此调用，PEP 收到 PEP_DPM_REGISTER_DEVICE 通知。

注册成功后，该驱动程序有机会初始化其组件， (例如，设置活动、更新延迟要求、更新预期空闲派驻服务等 ) 。 当驱动程序完成任何初始化任务后，它将通过调用 PoFxStartDevicePowerManagement 通知电源管理器。 在响应中，PEP 会收到 PEP_DPM_DEVICE_STARTED 通知。 此时，该设备被视为完全启用了运行时电源管理。

因此，PEP 无法向驱动程序发出任何电源控制请求，除非它首先收到 PEP_DPM_DEVICE_STARTED 通知或 PEP_DPM_POWER_CONTROL_REQUEST 通知。

>[!NOTE]
>如果 PEP 未发出任何电源控制请求，则 PEP 可以忽略此通知。

对于 PEP_DPM_DEVICE_STARTED 通知，AcceptDeviceNotification 例程以 IRQL <= DISPATCH_LEVEL 调用。

### <a name="pep_dpm_notify_component_idle_state"></a>PEP_DPM_NOTIFY_COMPONENT_IDLE_STATE

#### <a name="notification-pep_dpm_notify_component_idle_state"></a>通知 (PEP_DPM_NOTIFY_COMPONENT_IDLE_STATE) 

PEP_DPM_NOTIFY_COMPONENT_IDLE_STATE 的值。

#### <a name="data-pep_dpm_notify_component_idle_state"></a>数据 (PEP_DPM_NOTIFY_COMPONENT_IDLE_STATE) 

指向 [PEP_NOTIFY_COMPONENT_IDLE_STATE](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_notify_component_idle_state) 结构的指针。

当 OS 发出给定组件的空闲状态转换时，发送到 PEP。

当 OS 发出给定组件的空闲状态转换时，Windows 电源管理框架 (PoFx) 发送此通知。

>[!IMPORTANT]
>PEP 必须处理此通知。

对于每个空闲状态转换，在收到驱动程序之前和之后都会通知 PEP。 PEP 通过检查 PEP_NOTIFY_COMPONENT_IDLE_STATE 结构的 DriverNotified 成员来区分 pre 和 post 通知。 对于后通知，DriverNotified 成员将为 TRUE。

在转换为 F0 时通常使用预先通知。 在这种情况下，PEP 可能需要重新启用时钟或电源资源，以便当驱动程序处理 F0 通知时，硬件可用。 因此，在从 F0 过渡到更深层空闲状态时，通常使用后通知。 驱动程序处理空闲状态通知后，PEP 可以安全地关闭时钟和电源资源。

如果操作需要很长的时间，或者 IRQL 太大，无法同步完成转换，处理给定组件的空闲状态转换可能需要异步处理。 因此，PEP 可以通过将完成的成员分别设置为 TRUE 或 FALSE，同步或异步完成此通知。

如果通知将以异步方式完成，则 PEP 会请求工作 (参阅 RequestWorker) 并使用工作类型 PepWorkCompleteIdleState 在生成的 PEP_DPM_WORK 通知中填写提供的工作信息结构，从而在完成后通知 OS。

若要发送 PEP_DPM_NOTIFY_COMPONENT_IDLE_STATE 通知，PoFx 将调用 PEP 的 AcceptDeviceNotification 回调例程。 此例程在 IRQL <= DISPATCH_LEVEL 中调用。

### <a name="pep_dpm_register_debugger"></a>PEP_DPM_REGISTER_DEBUGGER

#### <a name="notification-pep_dpm_register_debugger"></a>通知 (PEP_DPM_REGISTER_DEBUGGER) 

PEP_DPM_REGISTER_DEBUGGER 的值。

#### <a name="data-pep_dpm_register_debugger"></a>数据 (PEP_DPM_REGISTER_DEBUGGER) 

指向 [PEP_REGISTER_DEBUGGER](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_register_debugger) 结构的指针。

通知 PEP：注册的设备可能用作调试端口。

Windows 电源管理框架 (PoFx) 发送此通知以通知 PEP，已注册的设备可能用作调试端口。

对于 PEP_DPM_REGISTER_DEBUGGER 通知，AcceptDeviceNotification 例程以 IRQL <= DISPATCH_LEVEL 调用。

### <a name="pep_dpm_low_power_epoch"></a>PEP_DPM_LOW_POWER_EPOCH

#### <a name="notification-pep_dpm_low_power_epoch"></a>通知 (PEP_DPM_LOW_POWER_EPOCH) 

PEP_DPM_LOW_POWER_EPOCH 的值。

#### <a name="data-pep_dpm_low_power_epoch"></a>数据 (PEP_DPM_LOW_POWER_EPOCH) 

指向 [PEP_LOW_POWER_EPOCH](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_low_power_epoch) 结构的指针。

此通知已弃用。

### <a name="pep_dpm_register_crashdump_device"></a>PEP_DPM_REGISTER_CRASHDUMP_DEVICE

#### <a name="notification-pep_dpm_register_crashdump_device"></a>通知 (PEP_DPM_REGISTER_CRASHDUMP_DEVICE) 

PEP_DPM_REGISTER_CRASHDUMP_DEVICE 的值。

#### <a name="data-pep_dpm_register_crashdump_device"></a>数据 (PEP_DPM_REGISTER_CRASHDUMP_DEVICE) 

指向 [PEP_REGISTER_CRASHDUMP_DEVICE](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_register_crashdump_device) 结构的指针。

Windows 电源管理框架 (PoFx) 在设备注册为故障转储处理程序时发送此通知。

当系统遇到严重错误时，生成内存转储)  (故障转储的功能对于确定崩溃原因非常有用。 默认情况下，当系统遇到错误检测时，Windows 将生成故障转储。 在这种情况下，系统处于一个非常受限制的操作环境中，禁用中断并且 HIGH_LEVEL 的系统 IRQL。

由于在将故障转储写入到磁盘 (即存储控制器、PCI 控制器 ) 等）中涉及的设备可能会在发生故障时关闭，因此，操作系统必须调入 PEP 才能打开设备。 这样，操作系统就会向故障转储堆栈上每台设备的 PEP 请求一个回调 (PowerOnDumpDeviceCallback) ，并在生成转储文件时调用回调。

在发生崩溃时，根据受约束的环境，PEP 提供的回调不得访问分页代码、阻止任何事件或调用任何可能执行相同操作的代码。 而且，启动任何所需资源的过程不会依赖于中断。 因此，在需要等待不同资源的启用时，PEP 可能需要恢复到轮询。 如果 PEP 无法在设备上打开这些约束，则不应处理通知或不提供回调例程。

若要发送 PEP_DPM_REGISTER_CRASHDUMP_DEVICE 通知，PoFx 将调用 PEP 的 AcceptDeviceNotification 回调例程。 对于此通知，AcceptDeviceNotification 例程在 IRQL <= HIGH_LEVEL 中调用。

### <a name="pep_dpm_device_idle_constraints"></a>PEP_DPM_DEVICE_IDLE_CONSTRAINTS

#### <a name="notification-pep_dpm_device_idle_constraints"></a>通知 (PEP_DPM_DEVICE_IDLE_CONSTRAINTS) 

PEP_DPM_DEVICE_IDLE_CONSTRAINTS 的值。

#### <a name="data-pep_dpm_device_idle_constraints"></a>数据 (PEP_DPM_DEVICE_IDLE_CONSTRAINTS) 

指向 [PEP_DEVICE_PLATFORM_CONSTRAINTS](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_device_platform_constraints) 结构的指针。
发送到 PEP 以查询设备 D 状态和平台空闲状态之间的依赖关系。

Windows 电源管理框架 (PoFx) 将此通知发送到 PEP，以查询设备 D 状态和平台空闲状态之间的依赖关系。 PEP 使用此通知返回设备仍可处于最浅的 D 状态，并进入每个平台空闲状态。 在进入关联的平台空闲状态之前，OS 将保证设备处于最小的 D 状态。 如果平台空闲状态不依赖于此设备处于任何 D 状态，则 PEP 应指定 PowerDeviceD0 的最小 D 状态。 如果任何平台空闲状态都不依赖于此设备处于特定的 D 状态，则可以忽略此通知。

在 PEP 收到 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATES 通知之后，会将此通知发送到每个设备。

若要发送 PEP_DPM_DEVICE_IDLE_CONSTRAINTS 通知，PoFx 将调用 PEP 的 AcceptDeviceNotification 回调例程。 在此调用中，通知参数值为 PEP_DPM_DEVICE_IDLE_CONSTRAINTS，数据参数指向 PEP_DEVICE_PLATFORM_CONSTRAINTS 结构。

对于 PEP_DPM_DEVICE_IDLE_CONSTRAINTS 通知，AcceptDeviceNotification 例程始终调用 IRQL = DISPATCH_LEVEL。

### <a name="pep_dpm_component_idle_constraints"></a>PEP_DPM_COMPONENT_IDLE_CONSTRAINTS

#### <a name="notification-pep_dpm_component_idle_constraints"></a>通知 (PEP_DPM_COMPONENT_IDLE_CONSTRAINTS) 

PEP_DPM_COMPONENT_IDLE_CONSTRAINTS 的值。

#### <a name="data-pep_dpm_component_idle_constraints"></a>数据 (PEP_DPM_COMPONENT_IDLE_CONSTRAINTS) 

指向 [PEP_COMPONENT_PLATFORM_CONSTRAINTS](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_component_platform_constraints) 结构的指针。

发送到 PEP 以查询组件 F 状态和平台空闲状态之间的依赖关系。

Windows 电源管理框架 (PoFx) 将此通知发送到 PEP，以查询组件 F 状态和平台空闲状态之间的依赖关系。 PEP 使用此通知返回的 F 状态最浅，组件仍可处于中，并进入每个平台空闲状态。 操作系统将保证组件在进入关联平台空闲状态之前处于最低 F 状态。 如果平台空闲状态不依赖于处于任何 F 状态的此组件，则 PEP 应指定最小 F 状态为0。 如果平台空闲状态不依赖于此组件处于特定 F 状态，则可以忽略此通知。

比 D0 更深层的设备空闲约束比设备上组件的组件空闲状态更多。 对于给定的平台空闲状态索引，如果设备指定了设备空闲限制，则将忽略与该设备关联的所有组件的相应组件空闲约束。

在 PEP 收到 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATES 通知之后，会将此通知发送到每个设备上的每个组件。

若要发送 PEP_DPM_COMPONENT_IDLE_CONSTRAINTS 通知，PoFx 将调用 PEP 的 AcceptDeviceNotification 回调例程。 AcceptDeviceNotification 例程始终调用 IRQL = DISPATCH_LEVEL。

### <a name="pep_dpm_query_component_perf_capabilities"></a>PEP_DPM_QUERY_COMPONENT_PERF_CAPABILITIES

#### <a name="notification-pep_dpm_query_component_perf_capabilities"></a>通知 (PEP_DPM_QUERY_COMPONENT_PERF_CAPABILITIES) 

PEP_DPM_QUERY_COMPONENT_PERF_CAPABILITIES 的值。

#### <a name="data-pep_dpm_query_component_perf_capabilities"></a>数据 (PEP_DPM_QUERY_COMPONENT_PERF_CAPABILITIES) 

指向 [PEP_QUERY_COMPONENT_PERF_CAPABILITIES](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_query_component_perf_capabilities) 结构的指针。

通知 PEP 正在查询为组件定义的性能状态 (P 状态) 集的数目。

若要发送 PEP_DPM_QUERY_COMPONENT_PERF_CAPABILITIES 通知，PoFx 将调用 PEP 的 AcceptDeviceNotification 回调例程。 在此调用中，通知参数值为 PEP_DPM_QUERY_COMPONENT_PERF_CAPABILITIES，数据参数指向 PEP_QUERY_COMPONENT_PERF_CAPABILITIES 结构。

对于 PEP_DPM_QUERY_COMPONENT_PERF_CAPABILITIES 通知，AcceptDeviceNotification 例程始终调用 IRQL = PASSIVE_LEVEL。

### <a name="pep_dpm_query_component_perf_set"></a>PEP_DPM_QUERY_COMPONENT_PERF_SET

#### <a name="notification-pep_dpm_query_component_perf_set"></a>通知 (PEP_DPM_QUERY_COMPONENT_PERF_SET) 

PEP_DPM_QUERY_COMPONENT_PERF_SET 的值。

#### <a name="data-pep_dpm_query_component_perf_set"></a>数据 (PEP_DPM_QUERY_COMPONENT_PERF_SET) 

指向 [PEP_QUERY_COMPONENT_PERF_SET](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_query_component_perf_set) 结构的指针。

通知 PEP 正在查询有关组件的一组性能状态值 (P 状态集) 的信息。

若要发送 PEP_DPM_QUERY_COMPONENT_PERF_SET 通知，PoFx 将调用 PEP 的 AcceptDeviceNotification 回调例程。 在此调用中，通知参数值为 PEP_DPM_QUERY_COMPONENT_PERF_SET，数据参数指向 PEP_QUERY_COMPONENT_PERF_SET 结构。

对于 PEP_DPM_QUERY_COMPONENT_PERF_SET 通知，AcceptDeviceNotification 例程始终调用 IRQL = PASSIVE_LEVEL。

### <a name="pep_dpm_query_component_perf_set_name"></a>PEP_DPM_QUERY_COMPONENT_PERF_SET_NAME

#### <a name="notification-opep_dpm_query_component_perf_set_name"></a>通知 (OPEP_DPM_QUERY_COMPONENT_PERF_SET_NAME) 

PEP_DPM_QUERY_COMPONENT_PERF_SET_NAME 的值。

#### <a name="data-opep_dpm_query_component_perf_set_name"></a>数据 (OPEP_DPM_QUERY_COMPONENT_PERF_SET_NAME) 

指向 [PEP_QUERY_COMPONENT_PERF_SET_NAME](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_query_component_perf_set_name) 结构的指针。

通知 PEP 正在查询有关组件的一组性能状态值 (P 状态集) 的信息。

若要发送 PEP_DPM_QUERY_COMPONENT_PERF_SET_NAME 通知，PoFx 将调用 PEP 的 AcceptDeviceNotification 回调例程。 在此调用中，通知参数值为 PEP_DPM_QUERY_COMPONENT_PERF_SET_NAME，数据参数指向 PEP_QUERY_COMPONENT_PERF_SET_NAME 结构。

对于 PEP_DPM_QUERY_COMPONENT_PERF_SET_NAME 通知，AcceptDeviceNotification 例程始终调用 IRQL = PASSIVE_LEVEL。

### <a name="pep_dpm_query_component_perf_states"></a>PEP_DPM_QUERY_COMPONENT_PERF_STATES

#### <a name="notification-pep_dpm_query_component_perf_states"></a>通知 (PEP_DPM_QUERY_COMPONENT_PERF_STATES) 

PEP_DPM_QUERY_COMPONENT_PERF_STATES 的值。

#### <a name="data-pep_dpm_query_component_perf_states"></a>数据 (PEP_DPM_QUERY_COMPONENT_PERF_STATES) 

指向 [PEP_QUERY_COMPONENT_PERF_STATES](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_query_component_perf_states) 结构的指针。

通知 PEP 正在查询它的一系列离散性能状态 (P-state) 指定 P 状态集的值。

若要发送 PEP_DPM_QUERY_COMPONENT_PERF_STATES 通知，PoFx 将调用 PEP 的 AcceptDeviceNotification 回调例程。 在此调用中，通知参数值为 PEP_DPM_QUERY_COMPONENT_PERF_STATES，数据参数指向 PEP_QUERY_COMPONENT_PERF_STATES 结构。

对于 PEP_DPM_QUERY_COMPONENT_PERF_STATES 通知，AcceptDeviceNotification 例程始终调用 IRQL = PASSIVE_LEVEL。

### <a name="pep_dpm_register_component_perf_states"></a>PEP_DPM_REGISTER_COMPONENT_PERF_STATES

#### <a name="notification-pep_dpm_register_component_perf_states"></a>通知 (PEP_DPM_REGISTER_COMPONENT_PERF_STATES) 

PEP_DPM_REGISTER_COMPONENT_PERF_STATES 的值。

#### <a name="data-pep_dpm_register_component_perf_states"></a>数据 (PEP_DPM_REGISTER_COMPONENT_PERF_STATES) 

指向 [PEP_REGISTER_COMPONENT_PERF_STATES](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_register_component_perf_states) 结构的指针。

通知 PEP 有关指定组件的 P 状态 (状态) 的性能状态。

若要发送 PEP_DPM_REGISTER_COMPONENT_PERF_STATES 通知，PoFx 将调用 PEP 的 AcceptDeviceNotification 回调例程。 在此调用中，通知参数值为 PEP_DPM_REGISTER_COMPONENT_PERF_STATES，数据参数指向 PEP_REGISTER_COMPONENT_PERF_STATES 结构。

对于 PEP_DPM_REGISTER_COMPONENT_PERF_STATES 通知，AcceptDeviceNotification 例程始终调用 IRQL = PASSIVE_LEVEL。

### <a name="pep_dpm_request_component_perf_state"></a>PEP_DPM_REQUEST_COMPONENT_PERF_STATE

#### <a name="notification-pep_dpm_request_component_perf_state"></a>通知 (PEP_DPM_REQUEST_COMPONENT_PERF_STATE) 

PEP_DPM_REQUEST_COMPONENT_PERF_STATE 的值。

#### <a name="data-pep_dpm_request_component_perf_state"></a>数据 (PEP_DPM_REQUEST_COMPONENT_PERF_STATE) 

指向 PEP_REQUEST_COMPONENT_PERF_STATE 结构的指针。

通知 PEP) Windows 电源管理框架 (PoFx) 请求一个或多个性能状态 (P 状态更改。

若要发送 PEP_DPM_REQUEST_COMPONENT_PERF_STATE 通知，PoFx 将调用 PEP 的 AcceptDeviceNotification 回调例程。 在此调用中，通知参数值为 PEP_DPM_REQUEST_COMPONENT_PERF_STATE，数据参数指向 PEP_REQUEST_COMPONENT_PERF_STATE 结构。

对于 PEP_DPM_REQUEST_COMPONENT_PERF_STATE 通知，AcceptDeviceNotification 例程始终调用 IRQL = PASSIVE_LEVEL。

### <a name="pep_dpm_query_current_component_perf_state"></a>PEP_DPM_QUERY_CURRENT_COMPONENT_PERF_STATE

#### <a name="notification-pep_dpm_query_current_component_perf_state"></a>通知 (PEP_DPM_QUERY_CURRENT_COMPONENT_PERF_STATE) 

PEP_DPM_QUERY_CURRENT_COMPONENT_PERF_STATE 的值。

#### <a name="data-pep_dpm_query_current_component_perf_state"></a>数据 (PEP_DPM_QUERY_CURRENT_COMPONENT_PERF_STATE) 

指向 PEP_QUERY_CURRENT_COMPONENT_PERF_STATE 结构的指针。

通知 PEP 正在查询有关指定 P 状态集内当前 P 状态的信息。

若要发送 PEP_DPM_QUERY_CURRENT_COMPONENT_PERF_STATE 通知，PoFx 将调用 PEP 的 AcceptDeviceNotification 回调例程。 在此调用中，通知参数值为 PEP_DPM_QUERY_CURRENT_COMPONENT_PERF_STATE，数据参数指向 PEP_QUERY_CURRENT_COMPONENT_PERF_STATE 结构。

对于 PEP_DPM_QUERY_CURRENT_COMPONENT_PERF_STATE 通知，AcceptDeviceNotification 例程始终调用 IRQL = PASSIVE_LEVEL。

### <a name="pep_dpm_query_debugger_transition_requirements"></a>PEP_DPM_QUERY_DEBUGGER_TRANSITION_REQUIREMENTS

#### <a name="notification-pep_dpm_query_debugger_transition_requirements"></a>通知 (PEP_DPM_QUERY_DEBUGGER_TRANSITION_REQUIREMENTS) 

PEP_DPM_QUERY_DEBUGGER_TRANSITION_REQUIREMENTS 的值。

#### <a name="data-pep_dpm_query_debugger_transition_requirements"></a>数据 (PEP_DPM_QUERY_DEBUGGER_TRANSITION_REQUIREMENTS) 

指向 [PEP_DEBUGGER_TRANSITION_REQUIREMENTS](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_debugger_transition_requirements) 结构的指针。

发送到 PEP 以查询需要关闭调试器的协调或平台状态集。

Windows 电源管理框架 (PoFx) 将此通知发送到 PEP，以查询需要关闭调试器的协调或平台状态集。 如果接受此通知，则操作系统将执行 PEP 的所有调试器电源转换，并且 PEP 不能使用 TransitionCriticalResource 来管理调试器。

在 PEP 接受 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 或 PEP_NOTIFY_PPM_QUERY_COORDINATED_STATES 通知之后，会向每个调试器设备发送此通知。

若要发送 PEP_DPM_QUERY_DEBUGGER_TRANSITION_REQUIREMENTS 通知，PoFx 将调用 PEP 的 AcceptDeviceNotification 回调例程。 对于此通知，AcceptDeviceNotification 例程始终调用 IRQL = DISPATCH_LEVEL。

### <a name="pep_dpm_query_soc_subsystem"></a>PEP_DPM_QUERY_SOC_SUBSYSTEM

#### <a name="notification-pep_dpm_query_soc_subsystem"></a>通知 (PEP_DPM_QUERY_SOC_SUBSYSTEM) 

PEP_DPM_QUERY_SOC_SUBSYSTEM 的值。

#### <a name="data-pep_dpm_query_soc_subsystem"></a>数据 (PEP_DPM_QUERY_SOC_SUBSYSTEM) 

指向 [PEP_QUERY_SOC_SUBSYSTEM](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_query_soc_subsystem) 结构的指针。

发送到 PEP，收集芯片 (SoC) 子系统的特定系统的基本信息。

在初始化了平台空闲状态之后，Windows 电源管理框架 (PoFx) 会将此通知发送到 PEP，以便收集有关特定 SoC 子系统的基本信息。 如果 PEP 未实现 SoC 子系统记帐，或未在指定的平台空闲状态下实现它，则返回 FALSE。 这会指示 OS 停止将诊断通知发送到此平台空闲状态的 PEP。

系统的 SubsystemCount 和子系统的 MetadataCount 可能会随 PEP/BSP 更新而更改。 每次操作系统启动时，SubsystemIndex 可能会更改。

>[!IMPORTANT]
>PEP 无法忽略此通知。 PEP 正在接收此通知，因为它使用非零 SubsystemCount 响应了此 PlatformIdleStateIndex 的 PEP_DPM_QUERY_SOC_SUBSYSTEM_COUNT 通知。

若要发送 PEP_DPM_QUERY_SOC_SUBSYSTEM 通知，PoFx 将以 IRQL < DISPATCH_LEVEL 调用 PEP 的 AcceptDeviceNotification 回调例程。

### <a name="pep_dpm_query_soc_subsystem_blocking_time"></a>PEP_DPM_QUERY_SOC_SUBSYSTEM_BLOCKING_TIME

#### <a name="notification-pep_dpm_query_soc_subsystem_blocking_time"></a>通知 (PEP_DPM_QUERY_SOC_SUBSYSTEM_BLOCKING_TIME) 

PEP_DPM_QUERY_SOC_SUBSYSTEM_BLOCKING_TIME 的值。

#### <a name="data-pep_dpm_query_soc_subsystem_blocking_time"></a>数据 (PEP_DPM_QUERY_SOC_SUBSYSTEM_BLOCKING_TIME) 

指向 [PEP_QUERY_SOC_SUBSYSTEM_BLOCKING_TIME](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_query_soc_subsystem_blocking_time) 结构的指针。

当操作系统需要收集芯片 (SoC 上的特定系统时间的统计信息时发送到 PEP) 子系统已阻止进入特定平台空闲状态，而无需操作系统的知识。

通常，操作系统会在扩展连接备用会话结束时调用此通知，其中 OS 尝试进入指定的平台空闲状态。 PEP_QUERY_SOC_SUBSYSTEM_COUNT。SubsystemCount 值，在子组件初始化期间由 PEP 填写，指定一次向 PEP 发送多少 PEP_DPM_QUERY_SOC_SUBSYSTEM_BLOCKING_TIME 通知。 PEP 可以接收给定子系统的多个 PEP_DPM_QUERY_SOC_SUBSYSTEM_BLOCKING_TIME 通知。 这些通知可能与 PEP_DPM_RESET_SOC_SUBSYSTEM_ACCOUNTING 通知交错在一起。

>[!IMPORTANT]
>PEP 无法忽略此通知。 PEP 正在接收此通知，因为它使用非零 SubsystemCount 响应了此 PlatformIdleStateIndex 的 PEP_DPM_QUERY_SOC_SUBSYSTEM_COUNT 通知。

若要发送 PEP_DPM_QUERY_SOC_SUBSYSTEM_BLOCKING_TIME 通知，PoFx 将以 IRQL < DISPATCH_LEVEL 调用 PEP 的 AcceptDeviceNotification 回调例程。

### <a name="pep_dpm_query_soc_subsystem_count"></a>PEP_DPM_QUERY_SOC_SUBSYSTEM_COUNT

#### <a name="notification-pep_dpm_query_soc_subsystem_count"></a>通知 (PEP_DPM_QUERY_SOC_SUBSYSTEM_COUNT) 

PEP_DPM_QUERY_SOC_SUBSYSTEM_COUNT 的值。

#### <a name="data-pep_dpm_query_soc_subsystem_count"></a>数据 (PEP_DPM_QUERY_SOC_SUBSYSTEM_COUNT) 

指向 [PEP_QUERY_SOC_SUBSYSTEM_COUNT](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_query_soc_subsystem_count) 结构的指针。

在已初始化平台空闲状态后发送到 PEP，告诉操作系统 PEP 是否支持针对给定平台空闲状态的芯片 (SoC) 子系统。

这是发送到 PEP 的第一个 SoC 子系统诊断通知。 如果 PEP 未实现 SoC 子系统记帐，或未在指定的平台空闲状态下实现它，则返回 FALSE，在这种情况下，操作系统将不会向 PEP 发送此平台空闲状态的更多的 SoC 子系统诊断通知。

>[!NOTE]
>如果 PEP 未实现针对指定平台空闲状态的 SoC 诊断通知，则它可以忽略此通知。

若要发送 PEP_DPM_QUERY_SOC_SUBSYSTEM_COUNT 通知，PoFx 将以 IRQL < DISPATCH_LEVEL 调用 PEP 的 AcceptDeviceNotification 回调例程。

### <a name="pep_dpm_query_soc_subsystem_metadata"></a>PEP_DPM_QUERY_SOC_SUBSYSTEM_METADATA

#### <a name="notification-pep_dpm_query_soc_subsystem_metadata"></a>通知 (PEP_DPM_QUERY_SOC_SUBSYSTEM_METADATA) 

PEP_DPM_QUERY_SOC_SUBSYSTEM_METADATA 的值。

#### <a name="data-pep_dpm_query_soc_subsystem_metadata"></a>数据 (PEP_DPM_QUERY_SOC_SUBSYSTEM_METADATA) 

指向 PEP_QUERY_SOC_SUBSYSTEM_METADATA 结构的指针。

发送到 PEP，收集有关刚刚查询阻塞时间的子系统的可选元数据。

此通知通常会在 PEP_DPM_QUERY_SOC_SUBSYSTEM_BLOCKING_TIME 通知之后立即发送到 PEP。 一个 PEP_DPM_QUERY_SOC_SUBSYSTEM_METADATA 通知收集描述子系统的所有键/值元数据对。

>[!IMPORTANT]
>PEP 无法忽略此通知。 PEP 正在接收此通知，因为它使用非零 SubsystemCount 响应了此 PlatformIdleStateIndex 的 PEP_DPM_QUERY_SOC_SUBSYSTEM_COUNT 通知。

若要发送 PEP_DPM_QUERY_SOC_SUBSYSTEM_METADATA 通知，PoFx 将调用 PEP 的 AcceptDeviceNotification 回调例程。 对于此通知，AcceptDeviceNotification 例程在 DISPATCH_LEVEL 的 IRQL < 调用。

### <a name="pep_dpm_reset_soc_subsystem_accounting"></a>PEP_DPM_RESET_SOC_SUBSYSTEM_ACCOUNTING

#### <a name="notification-pep_dpm_reset_soc_subsystem_accounting"></a>通知 (PEP_DPM_RESET_SOC_SUBSYSTEM_ACCOUNTING) 

PEP_DPM_RESET_SOC_SUBSYSTEM_ACCOUNTING 的值。

#### <a name="data-pep_dpm_reset_soc_subsystem_accounting"></a>数据 (PEP_DPM_RESET_SOC_SUBSYSTEM_ACCOUNTING) 

指向指向 [PEP_RESET_SOC_SUBSYSTEM_ACCOUNTING](/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_reset_soc_subsystem_accounting) 结构的指针的指针。 构造.

发送到 PEP 以清除所有子系统阻塞时间和元数据记帐，执行所需的任何附加初始化，然后重新启动记帐。

Windows 电源管理框架 (PoFx) 将在所有子系统都用 OS 初始化之后，随时将此通知发送到 PEP。 通常情况下，当操作系统开始新的分析时间段时，将会调用此通知， (SoC) 指定平台空闲状态，在进入连接备用) 时 (目标为 DRIPS。 操作系统仅为 PEP 为其初始化了一个或多个 SoC 子系统的平台空闲状态发送此通知。

若要发送 PEP_DPM_RESET_SOC_SUBSYSTEM_ACCOUNTING 通知，PoFx 将以 IRQL < DISPATCH_LEVEL 调用 PEP 的 AcceptDeviceNotification 回调例程。
