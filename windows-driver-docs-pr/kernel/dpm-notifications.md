---
title: 设备电源管理 (DPM) 通知
description: PEP AcceptDeviceNotification 回调例程接收每个设备电源管理 (DPM) 通知都伴有一个通知参数，指示通知的类型和指向数据的数据参数结构包含指定的通知类型的信息。
ms.assetid: 47B487A3-2707-4B0F-BD61-8C4A89F99AE1
keywords:
- AcceptDeviceNotification
ms.date: 01/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 984444958b8a4ae24edcfa04188933fe7aefc204
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387178"
---
# <a name="device-power-management-dpm-notifications"></a>设备电源管理 (DPM) 通知

PEP AcceptDeviceNotification 回调例程接收每个设备电源管理 (DPM) 通知都伴有一个通知参数，指示通知的类型和指向数据的数据参数结构包含指定的通知类型的信息。

在此调用，通知参数设置为 PEP_DPM_XXX 常量值，该值指示通知类型。 数据参数指向与此通知类型相关联的 PEP_XXX 结构类型。

使用以下 DPM 通知 Id AcceptDeviceNotification 回调例程。

## <a name="pepdpmpreparedevice"></a>PEP_DPM_PREPARE_DEVICE 

通知 PEP_DPM_PREPARE_DEVICE 的值。

指向 PEP_PREPARE_DEVICE 结构数据的指针。
告知拥有指定的设备中 D0 配置使设备能够运行 PEP （工作） 设备电源状态。

设备的驱动程序堆栈由操作系统在首次启动之前，Windows 电源管理框架 (PoFx) 会将此通知发送到 PEP。 此通知允许 PEP，打开任何外部电源或时钟资源所需操作设备。

若要发送 PEP_DPM_PREPARE_DEVICE 通知，操作系统将调用 PEP AcceptDeviceNotification 回调例程。 在此调用，通知参数值为 PEP_DPM_PREPARE_DEVICE，且数据参数指向 PEP_PREPARE_DEVICE 结构。 在进入时，此结构的 DeviceId 成员是唯一标识设备的设备标识字符串。 再返回，PEP 设置为 true 声明所有权的设备，或为 FALSE，则此结构的 DeviceAccepted 成员，以指示它不拥有该设备。

拥有设备的电源管理 PEP 负责管理的是外部的设备和操作设备所需的电源和时钟的资源。 此 PEP 启用时钟信号和 PEP_DPM_PREPARE_DEVICE 通知，响应中的设备的电源，以及从 PEP_DPM_ABANDON_DEVICE 通知响应中的设备中删除的时钟信号和能力。

下表显示了当此操作系统将 PEP_DPM_PREPARE_DEVICE 通知发送到 PEP，实际上是前置条件和后 PEP 处理此通知它所拥有的设备，必须实际上在后置条件。


设备可以是任何电源状态下的前置条件。 如果 PEP 声明设备的所有权，设备及其所有组件必须打开，并且必须 ungated 到设备的时钟后, 置条件。 PEP 可以接收多个设备的 PEP_DPM_PREPARE_DEVICE 通知作为此电源管理器尝试找到 PEP 所有者为这些设备。 PEP 应将 PEP_PREPARE_DEVICE 结构的 DeviceAccepted 成员设置为 FALSE 的 PEP 不拥有的所有设备。

不 PEP_DPM_PREPARE_DEVICE 会发送通知的核心设备。

对于 PEP_DPM_PREPARE_DEVICE 通知，AcceptDeviceNotification 例程始终在调用 IRQL = passive_level 调用。
 
## <a name="pepdpmabandondevice"></a>PEP_DPM_ABANDON_DEVICE 
通知 PEP_DPM_ABANDON_DEVICE 的值。

指向 PEP_ABANDON_DEVICE 结构数据的指针。
告知 PEP 不再使用指定的设备操作系统。

操作系统中删除设备的驱动程序堆栈后，Windows 电源管理框架 (PoFx) 会将此通知发送到 PEP。 此通知允许 PEP 关闭任何外部电源或用于运行设备，并从未来决策制定过程中删除此设备的时钟资源。 如果稍后必须重新启动设备，PEP 会首先收到 PEP_DPM_PREPARE_DEVICE 通知。

若要发送 PEP_DPM_ABANDON_DEVICE 通知，操作系统将调用 PEP AcceptDeviceNotification 回调例程。 在此调用，通知参数值为 PEP_DPM_ABANDON_DEVICE，且数据参数指向 PEP_ABANDON_DEVICE 结构。 在进入时，此结构的 DeviceId 成员是唯一标识设备的设备标识字符串。 再返回，PEP 设置为 true 声明所有权的设备，或为 FALSE，则此结构的 DeviceAccepted 成员，以指示它不拥有该设备。

拥有设备的电源管理 PEP 负责管理的是外部的设备和操作设备所需的电源和时钟的资源。

下表显示了当此操作系统将 PEP_DPM_ABANDON_DEVICE 通知发送到 PEP，实际上是前置条件和后 PEP 处理此通知它所拥有的设备，必须实际上在后置条件。


前置条件 PEP 已收到的设备和设备的接受的所有权的 PEP_DPM_PREPARE_DEVICE 通知。 如果收到的设备的 PEP_DPM_REGISTER_DEVICE 通知 PEP 并接受设备注册，它随后已收到 PEP_DPM_UNREGISTER_DEVICE 通知设备。 后置条件，必须释放对 PEP_DPM_PREPARE_DEVICE 通知响应中分配的任何资源。 对于 PEP_DPM_PREPARE_DEVICE 通知，AcceptDeviceNotification 例程始终在调用 IRQL = passive_level 调用。
 
## <a name="pepdpmregisterdevice"></a>PEP_DPM_REGISTER_DEVICE 
通知 PEP_DPM_REGISTER_DEVICE 的值。

指向 PEP_REGISTER_DEVICE_V2 结构数据的指针。
告知 PEP 与 Windows 电源管理框架 (PoFx) 已注册指定的设备驱动程序堆栈。

当设备的驱动程序堆栈调用 PoFxRegisterDevice 例程来注册设备时，PoFx 将发送此通知。 此通知允许 PEP 将设备的注册信息复制到 PEP 的内部存储以供日后参考。

若要发送 PEP_DPM_REGISTER_DEVICE 通知，操作系统将调用 PEP AcceptDeviceNotification 回调例程。 在此调用，通知参数值为 PEP_DPM_REGISTER_DEVICE，且数据参数指向包含设备的内核句柄和其他注册信息的 PEP_REGISTER_DEVICE_V2 结构。 在进入时，此结构的 DeviceId 成员是唯一标识设备的设备标识字符串。 再返回，PEP 设置为 true 声明所有权的设备，或为 FALSE，则此结构的 DeviceAccepted 成员，以指示它不拥有该设备。 有关此结构的其他成员的信息，请参阅 PEP_REGISTER_DEVICE_V2。

下表显示了当此操作系统将 PEP_DPM_REGISTER_DEVICE 通知发送到 PEP，实际上是前置条件和后 PEP 处理此通知它所拥有的设备，必须实际上在后置条件。

条件类型说明的前置条件 PEP 已收到 PEP_DPM_PREPARE_DEVICE 通知它所拥有的设备。 后置条件 PEP 已准备好接收与此设备关联其他设备电源管理 (DPM) 通知。 

 

对于 PEP_DPM_REGISTER_DEVICE 通知，AcceptDeviceNotification 例程始终在调用 IRQL = passive_level 调用。
 
## <a name="pepdpmunregisterdevice"></a>PEP_DPM_UNREGISTER_DEVICE 
通知 PEP_DPM_UNREGISTER_DEVICE 的值。

指向 PEP_UNREGISTER_DEVICE 结构数据的指针。
告知 PEP 拥有指定的设备的驱动程序堆栈已从 Windows 电源管理框架 (PoFx) 提取其注册的设备。

PoFx 将发送此通知来通知 PEP PEP 在前一次 PEP_DPM_REGISTER_DEVICE 通知期间存储的任何注册信息将不再有效。 在响应中，PEP 可以清理此设备的电源管理的任何内部状态。

若要发送 PEP_DPM_UNREGISTER_DEVICE 通知，操作系统将调用 PEP AcceptDeviceNotification 回调例程。 在此调用，通知参数值为 PEP_DPM_UNREGISTER_DEVICE，且数据参数指向 PEP_UNREGISTER_DEVICE 结构。 此结构包含 PEP 中设备的上一个 PEP_DPM_REGISTER_DEVICE 通知响应创建句柄。

下表显示了当此操作系统将 PEP_DPM_UNREGISTER_DEVICE 通知发送到 PEP，实际上是前置条件和后 PEP 处理此通知它所拥有的设备，必须实际上在后置条件。


如果收到的设备的 PEP_DPM_REGISTER_DEVICE 通知并接受设备注册 PEP 前置条件。 PEP 可以接收任何与此设备关联的设备电源管理 (DPM) 通知。 PEP 可以报告"工作"与此设备关联。 后置条件 PEP 可以不会再收到与此设备，除了 PEP_DPM_ABANDON_DEVICE 关联任何设备电源管理 (DPM) 通知。 PEP 无法报告"工作"与此设备关联。 对于 PEP_DPM_UNREGISTER_DEVICE 通知，AcceptDeviceNotification 例程始终在调用 IRQL = passive_level 调用。
 
## <a name="pepdpmdevicepowerstate"></a>PEP_DPM_DEVICE_POWER_STATE 
通知 PEP_DPM_DEVICE_POWER_STATE 的值。

指向 PEP_DEVICE_POWER_STATE 结构数据的指针。
PEP 每次发送给设备的驱动程序堆栈或者请求更改到新的 Dx 电源状态，或以前请求的转换到 Dx 电源状态完成。

PEP 调用 RequestWorker 例程以请求工作项后，通过发送 PEP PEP_DPM_DEVICE_POWER_STATE 通知进行响应 PoFx。 但是，不发送此通知，直到有足够处理工作项所需的资源 （即，工作线程）。 这样一来，PoFx 保证，PEP 在通知期间将传递给 PoFx 工作请求可能永远不会失败由于资源不足。

若要发送 PEP_DPM_DEVICE_POWER_STATE 通知，操作系统将调用 PEP AcceptDeviceNotification 回调例程。 在此调用，通知参数值为 PEP_DPM_DEVICE_POWER_STATE，且数据参数指向 PEP_DEVICE_POWER_STATE 结构。 在进入时，PEP 应假定此结构的内容均未初始化。 若要处理此通知，PEP 应设置为指向描述所请求的工作的 PEP 分配 PEP_WORK_INFORMATION 结构 WorkInformation 成员。 此外，PEP 应设置为 TRUE 以确认 PEP 已处理 PEP_DEVICE_POWER_STATE 通知并且 WorkInformation 成员指向有效的 PEP_WORK_INFORMATION 结构 PEP_WORK 结构的 NeedWork 成员。 如果 PEP 失败以处理通知，或无法分配 PEP_WORK_INFORMATION 结构，PEP 应 WorkInformation 成员设置为 NULL，并将 NeedWork 成员设置为 FALSE。

对于 PEP_DPM_DEVICE_POWER_STATE 通知，AcceptDeviceNotification 例程始终在调用 IRQL = passive_level 调用。
 
## <a name="pepdpmcomponentactive"></a>PEP_DPM_COMPONENT_ACTIVE 
通知 PEP_DPM_COMPONENT_ACTIVE 的值。

数据： 指向 PEP_COMPONENT_ACTIVE 结构标识的组件，并且指示是否对活动的条件或空闲条件，此组件进行转换。
通知一个组件需要从空闲状态的条件的转换活动的条件，PEP，反之亦然。

当转换正在等待向活动的条件或空闲条件时，Windows 电源管理框架 (PoFx) 将发送此通知。 

若要发送 PEP_DPM_COMPONENT_ACTIVE 通知，PoFx 调用 PEP AcceptDeviceNotification 回调例程。 在此调用，通知参数值为 PEP_DPM_COMPONENT_ACTIVE，且数据参数指向 PEP_COMPONENT_ACTIVE 结构。

活动条件中是可访问的组件。 无法访问的组件处于空闲状态的条件。 在 F0 组件电源状态始终是处于活动状态的组件。 该组件不能离开 F0，直到进入空闲状态的条件。 处于空闲状态的组件可能是 F0 中或低功耗 Fx 状态中。 组件的活动/空闲条件是用于确定组件是否可访问的驱动程序的唯一可靠方法。 一个组件，它位于 F0 但处于空闲状态，还可能要切换到低功耗 Fx 状态。

准备好进入空闲状态的条件的活动的组件时，转换会立即发生。 在 PEP_DPM_COMPONENT_ACTIVE 通知的处理，PEP 可能，例如，请求转换从 F0 到低功耗 Fx 状态组件。

如果组件处于低功耗 Fx 状态 PEP_DPM_COMPONENT_ACTIVE 通知给活动条件从空闲条件请求转换时，PEP 必须先切换组件到 F0 之前该组件可输入的活动的条件。 PEP 可能需要完成以异步方式从 PEP_DPM_COMPONENT_ACTIVE 通知 AcceptDeviceNotification 回调返回后，准备为转换到活动的条件组件。 PEP 组件完全配置为在活动的条件操作后，必须调用 RequestWorker 例程，然后通过设置 WorkType 处理生成 PEP_DPM_WORK 通知 = PepWorkActiveComplete PEP_WORK_INFORMATION 结构中。

如果 PEP 收到 PEP_DPM_COMPONENT_ACTIVE 通知处于 F0，已完全配置为在活动的条件操作的组件，PEP 可能无法完成以同步方式处理此通知。 如果支持"的快速路径"通知的处理，则此通知的 PEP_COMPONENT_ACTIVE 结构 WorkInformation 成员包含 PEP_WORK_INFORMATION 结构的指针和 PEP 可以设置到此结构的 WorkType 成员PepWorkActiveComplete 完成转换。 但是，如果 WorkInformation = NULL，没有"快速路径"是可用，PEP 必须完成以异步方式通过调用 RequestWorker 过渡上, 一段中所述。

有关活动和空闲条件的详细信息，请参阅组件级别电源管理。

对于 PEP_DPM_COMPONENT_ACTIVE 通知，在 IRQL 调用 AcceptDeviceNotification 例程 < = DISPATCH_LEVEL。
 
## <a name="pepdpmwork"></a>PEP_DPM_WORK 
通知 PEP_DPM_WORK 的值。

指向 PEP_WORK 结构数据的指针。
每次 PEP 调用 RequestWorker 例程以请求从 Windows 电源管理框架 (PoFx) 的工作项后，发送到 PEP。

PEP 调用 RequestWorker 例程以请求工作项后，通过发送 PEP PEP_DPM_WORK 通知进行响应 PoFx。 但是，不发送此通知，直到有足够处理工作项所需的资源 （即，工作线程）。 这样一来，PoFx 保证，PEP 在通知期间将传递给 PoFx 工作请求可能永远不会失败由于资源不足。

若要发送 PEP_DPM_WORK 通知，操作系统将调用 PEP AcceptDeviceNotification 回调例程。 在此调用，通知参数值为 PEP_DPM_WORK，且数据参数指向 PEP_WORK 结构。 在进入时，PEP 应假定此结构的内容均未初始化。 若要处理此通知，PEP 应设置为指向描述所请求的工作的 PEP 分配 PEP_WORK_INFORMATION 结构 WorkInformation 成员。 此外，PEP 应设置为 TRUE 以确认 PEP 已处理 PEP_DPM_WORK 通知并且 WorkInformation 成员指向有效的 PEP_WORK_INFORMATION 结构 PEP_WORK 结构的 NeedWork 成员。 如果 PEP 失败以处理通知，或无法分配 PEP_WORK_INFORMATION 结构，PEP 应 WorkInformation 成员设置为 NULL，并将 NeedWork 成员设置为 FALSE。

对于 PEP_DPM_WORK 通知，AcceptDeviceNotification 例程始终在调用 IRQL = passive_level 调用。
 
## <a name="pepdpmpowercontrolrequest"></a>PEP_DPM_POWER_CONTROL_REQUEST 
通知 PEP_DPM_POWER_CONTROL_REQUEST 的值。

指向 PEP_POWER_CONTROL_REQUEST 结构数据的指针。
通知 PEP 驱动程序已调用 PoFxPowerControl API 来控制代码将直接发送到 PEP。

Windows 电源管理框架 (PoFx) 将此通知发送到 PEP，当驱动程序调用 PoFxPowerControl API 来控制代码将直接发送到 PEP。 通知数据指针在这种情况下指向 PEP_POWER_CONTROL_REQUEST 结构。 

电源控制请求以及它们的语义 PEP 编写器和设备类所有者之间定义。 通常，此类接口是设备类特定的通信的通用的电源管理框架中未捕获的。 例如，UART 控制器可能通信波特率汇率信息到 PEP 来修改一些平台时钟 rails/分隔线和此类通信可能会利用电源控制请求。 

请注意 PEP 只能请求后收到 PEP_DPM_DEVICE_STARTED 通知或 PEP_DPM_POWER_CONTROL_REQUEST 通知向设备发送控制代码。
 

对于 PEP_DPM_POWER_CONTROL_REQUEST 通知，在 IRQL 调用 AcceptDeviceNotification 例程 < = DISPATCH_LEVEL。
 
## <a name="pepdpmpowercontrolcomplete"></a>PEP_DPM_POWER_CONTROL_COMPLETE 
通知 PEP_DPM_POWER_CONTROL_COMPLETE 的值。

指向 PEP_POWER_CONTROL_COMPLETE 结构数据的指针。
通知 PEP 驱动程序已完成通过 PEP 以前颁发的电源控制请求

驱动程序完成之前发出 PEP 的电源控制请求时，Windows 电源管理框架 (PoFx) 会将此通知发送到 PEP。 

如果它不会发出任何电源控制请求，请注意 PEP 可以忽略此通知。
 
对于 PEP_DPM_POWER_CONTROL_COMPLETE 通知，在 IRQL 调用 AcceptDeviceNotification 例程 < = DISPATCH_LEVEL。
 
## <a name="pepdpmsystemlatencyupdate"></a>PEP_DPM_SYSTEM_LATENCY_UPDATE 
通知 PEP_DPM_SYSTEM_LATENCY_UPDATE 的值。

指向 PEP_SYSTEM_LATENCY 结构数据的指针。
通知操作系统已更新的整个系统滞后时间公差 PEP。

Windows 电源管理框架 (PoFx) 将操作系统更新整体系统延迟偏差匹配时发送此通知。 

在早期版本的 PoFx，此通知使用 PEP 处理器和平台空闲状态选择。 使用最新的 PEP 接口，则选择过程完全由操作系统处理和这种情况下此通知已不再有用。 它包含此处出于完整性的考虑，PEP 应忽略它。 

若要发送 PEP_DPM_SYSTEM_LATENCY_UPDATE 通知，PoFx 调用 PEP AcceptDeviceNotification 回调例程。 有关此通知，请在 IRQL 调用 AcceptDeviceNotification 例程 < = DISPATCH_LEVEL。
 
## <a name="pepdpmdevicestarted"></a>PEP_DPM_DEVICE_STARTED 
通知 PEP_DPM_DEVICE_STARTED 的值。

指向 PEP_DEVICE_STARTED 结构数据的指针。
通知 PEP 设备已启动，这样就可以接收电源控制事务。

设备堆栈注册运行时在两个步骤中的电源管理的操作系统。 该驱动程序首先调用 PoFxRegisterDevice 提供信息的组件，其空闲状态和相应的属性数。 在此调用的响应，PEP 会收到 PEP_DPM_REGISTER_DEVICE 通知。 

注册成功后，该驱动程序将有机会来初始化其组件 （即集处于活动状态、 更新延迟要求，应更新空闲驻留等）。 该驱动程序完成后的所有初始化任务，它将通过调用 PoFxStartDevicePowerManagement 通知电源管理器。 在响应中，PEP 会收到 PEP_DPM_DEVICE_STARTED 通知。 此时，设备被视为完全启用运行时电源管理的。 

因此，PEP 不能发出任何电源控制请求向驱动程序或者首次收到 PEP_DPM_DEVICE_STARTED 通知或 PEP_DPM_POWER_CONTROL_REQUEST 通知。 

如果它不会发出任何电源控制请求，请注意 PEP 可以忽略此通知。
 
对于 PEP_DPM_DEVICE_STARTED 通知，在 IRQL 调用 AcceptDeviceNotification 例程 < = DISPATCH_LEVEL。
 
## <a name="pepdpmnotifycomponentidlestate"></a>PEP_DPM_NOTIFY_COMPONENT_IDLE_STATE 
通知 PEP_DPM_NOTIFY_COMPONENT_IDLE_STATE 的值。

指向 PEP_NOTIFY_COMPONENT_IDLE_STATE 结构数据的指针。
操作系统问题给定组件的空闲状态转换时，发送到 PEP。 

操作系统问题给定组件的空闲状态转换时，Windows 电源管理框架 (PoFx) 将发送此通知。


重要 PEP 必须处理此通知。
 

对于每个空闲状态转换，PEP 是之前和之后会通知驱动程序收到通知。 PEP 区分通过检查 PEP_NOTIFY_COMPONENT_IDLE_STATE 结构的 DriverNotified 成员的 pre 和 post 通知。 对于后通知，DriverNotified 成员将为 TRUE。

当转换到 F0，通常使用前通知。 在这种情况下 PEP 可能需要重新启用时钟或电源资源，以便在硬件时，驱动程序处理 F0 通知，会提供。 相应地，F0 从转换到更深入的空闲状态时，通常使用后的通知。 驱动程序已处理的空闲状态通知后，PEP 安全地可以关闭时钟和强大功能的资源。 

处理给定组件的空闲状态转换可能需要异步处理操作需要很长时间或 IRQL 是否过高，以同步方式完成转换。 因此，PEP 可以完成此通知以同步方式还是以异步方式通过分别将已完成成员设置为 TRUE 或 FALSE。 

如果通知是以异步方式完成，PEP 会通过请求工作线程通知上完成的 OS （请参阅 RequestWorker） 并填写在生成 PEP_DPM_WORK 通知中使用的工作类型的提供的工作信息结构PepWorkCompleteIdleState。 

若要发送 PEP_DPM_NOTIFY_COMPONENT_IDLE_STATE 通知，PoFx 调用 PEP AcceptDeviceNotification 回调例程。 此例程称为在 IRQL < = DISPATCH_LEVEL。
 
## <a name="pepdpmregisterdebugger"></a>PEP_DPM_REGISTER_DEBUGGER 
通知 PEP_DPM_REGISTER_DEBUGGER 的值。

指向 PEP_REGISTER_DEBUGGER 结构数据的指针。
通知已注册的设备可用作调试端口 PEP。

Windows 电源管理框架 (PoFx) 将发送此通知来通知 PEP 已注册的设备可用作调试端口。 

对于 PEP_DPM_REGISTER_DEBUGGER 通知，在 IRQL 调用 AcceptDeviceNotification 例程 < = DISPATCH_LEVEL。
 
## <a name="pepdpmregistercrashdumpdevice"></a>PEP_DPM_REGISTER_CRASHDUMP_DEVICE 
通知 PEP_DPM_REGISTER_CRASHDUMP_DEVICE 的值。

指向 PEP_REGISTER_CRASHDUMP_DEVICE 结构数据的指针。
为故障转储处理程序注册设备时，Windows 电源管理框架 (PoFx) 将发送此通知。

当系统遇到致命错误时生成内存转储 （故障转储） 的功能是向确定在发生崩溃的原因非常有用。 Windows，默认情况下，将生成故障转储时系统遇到错误检查。 在此上下文中，系统在非常严格的操作环境下使用禁用的中断和系统在 HIGH_LEVEL IRQL。

由于设备涉及到故障转储写入磁盘 （即存储控制器、 PCI 控制器等） 可能会关闭在发生崩溃时，操作系统必须在设备上调用幂 PEP。 在这种情况下，OS 将从每个设备上的故障转储堆栈 PEP 请求回调 (PowerOnDumpDeviceCallback) 和生成转储文件时调用的回调。 

在崩溃时提供的受限制的环境，PEP 所提供的回调必须不分页的代码或阻止访问，任何事件上调用的任何代码都可能会执行相同的操作。 此外，增强了任何所需资源的过程不能依赖于中断。 因此，PEP 可能要还原为轮询它需要等待启用的各种资源。 如果 PEP 不能开启这些约束下设备时，它应不处理通知，或未提供回调例程。 

若要发送 PEP_DPM_REGISTER_CRASHDUMP_DEVICE 通知，PoFx 调用 PEP AcceptDeviceNotification 回调例程。 有关此通知，请在 IRQL 调用 AcceptDeviceNotification 例程 < = HIGH_LEVEL。
 
## <a name="pepdpmdeviceidleconstraints"></a>PEP_DPM_DEVICE_IDLE_CONSTRAINTS 
通知 PEP_DPM_DEVICE_IDLE_CONSTRAINTS 的值。

指向 PEP_DEVICE_PLATFORM_CONSTRAINTS 结构数据的指针。
发送到查询 PEP 进行设备 D 状态和平台空闲状态之间的依赖关系。

Windows 电源管理框架 (PoFx) 将此通知发送到 PEP D 状态的设备和平台空闲状态之间的依赖项的查询。 PEP 使用此通知返回最亮 D 态该设备仍然可以进行中并且输入每个平台的空闲状态。 操作系统可以保证在设备进入关联的平台空闲状态前处于最小的 D 状态。 如果平台闲置状态不依赖于此设备正在任何 D 状态，PEP 应指定 PowerDeviceD0 最小 D 状态。 如果没有平台空闲状态依赖于此设备正在某一特定 D 状态，则可以忽略此通知。 

PEP 收到 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATES 通知后，此通知是发送到每个设备。 

若要发送 PEP_DPM_DEVICE_IDLE_CONSTRAINTS 通知，PoFx 调用 PEP AcceptDeviceNotification 回调例程。 在此调用，通知参数值为 PEP_DPM_DEVICE_IDLE_CONSTRAINTS，且数据参数指向 PEP_DEVICE_PLATFORM_CONSTRAINTS 结构。

对于 PEP_DPM_DEVICE_IDLE_CONSTRAINTS 通知，AcceptDeviceNotification 例程始终在调用 IRQL = DISPATCH_LEVEL。
 
## <a name="pepdpmcomponentidleconstraints"></a>PEP_DPM_COMPONENT_IDLE_CONSTRAINTS 
通知 PEP_DPM_COMPONENT_IDLE_CONSTRAINTS 的值。

指向 PEP_COMPONENT_PLATFORM_CONSTRAINTS 结构数据的指针。
发送到查询 PEP 进行组件 F 状态和平台空闲状态之间的依赖关系。

Windows 电源管理框架 (PoFx) 将此通知发送到 PEP 组件 F 状态和平台空闲状态之间的依赖关系的查询。 PEP 使用此通知以返回的最亮 F-状态组件仍可进行中，以及输入每个平台的空闲状态。 操作系统将保证组件进入关联的平台空闲状态前处于最小的 F 状态。 如果平台闲置状态不依赖于任何 F 状态在此组件，PEP 应指定最小 F 状态为 0。 如果此组件正在某一特定的 F 状态不依赖于任何平台空闲状态，则可以忽略此通知。 

设备空闲约束深于 D0 是比组件在设备上的组件的空闲状态的多个约束。 对于给定的平台空闲状态索引，如果设备指定设备空闲约束，则忽略与设备关联的所有组件的相应组件空闲约束。 

PEP 接收 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATES 通知后，此通知是发送到每台设备上的每个组件。 

若要发送 PEP_DPM_COMPONENT_IDLE_CONSTRAINTS 通知，PoFx 调用 PEP AcceptDeviceNotification 回调例程。 AcceptDeviceNotification 例程始终调用在 IRQL = DISPATCH_LEVEL。
 
## <a name="pepdpmquerycomponentperfcapabilities"></a>PEP_DPM_QUERY_COMPONENT_PERF_CAPABILITIES 
通知 PEP_DPM_QUERY_COMPONENT_PERF_CAPABILITIES 的值。

指向 PEP_QUERY_COMPONENT_PERF_CAPABILITIES 结构数据的指针。
通知 PEP 它正被查询的组件定义的性能状态 （P 状态） 集的数量。

若要发送 PEP_DPM_QUERY_COMPONENT_PERF_CAPABILITIES 通知，PoFx 调用 PEP AcceptDeviceNotification 回调例程。 在此调用，通知参数值为 PEP_DPM_QUERY_COMPONENT_PERF_CAPABILITIES，且数据参数指向 PEP_QUERY_COMPONENT_PERF_CAPABILITIES 结构。

对于 PEP_DPM_QUERY_COMPONENT_PERF_CAPABILITIES 通知，AcceptDeviceNotification 例程始终在调用 IRQL = passive_level 调用。
 
## <a name="pepdpmquerycomponentperfset"></a>PEP_DPM_QUERY_COMPONENT_PERF_SET 
通知 PEP_DPM_QUERY_COMPONENT_PERF_SET 的值。

指向 PEP_QUERY_COMPONENT_PERF_SET 结构数据的指针。
通知 PEP 它正在查询的一组组件的性能状态值 （P 状态集） 有关的信息。

若要发送 PEP_DPM_QUERY_COMPONENT_PERF_SET 通知，PoFx 调用 PEP AcceptDeviceNotification 回调例程。 在此调用，通知参数值为 PEP_DPM_QUERY_COMPONENT_PERF_SET，且数据参数指向 PEP_QUERY_COMPONENT_PERF_SET 结构。

对于 PEP_DPM_QUERY_COMPONENT_PERF_SET 通知，AcceptDeviceNotification 例程始终在调用 IRQL = passive_level 调用。
 
## <a name="pepdpmquerycomponentperfsetname"></a>PEP_DPM_QUERY_COMPONENT_PERF_SET_NAME 
通知 PEP_DPM_QUERY_COMPONENT_PERF_SET_NAME 的值。

指向 PEP_QUERY_COMPONENT_PERF_SET_NAME 结构数据的指针。
通知 PEP 它正在查询的一组组件的性能状态值 （P 状态集） 有关的信息。

若要发送 PEP_DPM_QUERY_COMPONENT_PERF_SET_NAME 通知，PoFx 调用 PEP AcceptDeviceNotification 回调例程。 在此调用，通知参数值为 PEP_DPM_QUERY_COMPONENT_PERF_SET_NAME，且数据参数指向 PEP_QUERY_COMPONENT_PERF_SET_NAME 结构。

对于 PEP_DPM_QUERY_COMPONENT_PERF_SET_NAME 通知，AcceptDeviceNotification 例程始终在调用 IRQL = passive_level 调用。
 
## <a name="pepdpmquerycomponentperfstates"></a>PEP_DPM_QUERY_COMPONENT_PERF_STATES 
通知 PEP_DPM_QUERY_COMPONENT_PERF_STATES 的值。

指向 PEP_QUERY_COMPONENT_PERF_STATES 结构数据的指针。
通知 PEP 它正在查询的一系列离散的性能状态 （P 状态） 值的一组指定 P 状态。

若要发送 PEP_DPM_QUERY_COMPONENT_PERF_STATES 通知，PoFx 调用 PEP AcceptDeviceNotification 回调例程。 在此调用，通知参数值为 PEP_DPM_QUERY_COMPONENT_PERF_STATES，且数据参数指向 PEP_QUERY_COMPONENT_PERF_STATES 结构。

对于 PEP_DPM_QUERY_COMPONENT_PERF_STATES 通知，AcceptDeviceNotification 例程始终在调用 IRQL = passive_level 调用。
 
## <a name="pepdpmregistercomponentperfstates"></a>PEP_DPM_REGISTER_COMPONENT_PERF_STATES 
通知 PEP_DPM_REGISTER_COMPONENT_PERF_STATES 的值。

指向 PEP_REGISTER_COMPONENT_PERF_STATES 结构数据的指针。
有关指定组件的性能状态 （P 状态） 的信息通知 PEP。

若要发送 PEP_DPM_REGISTER_COMPONENT_PERF_STATES 通知，PoFx 调用 PEP AcceptDeviceNotification 回调例程。 在此调用，通知参数值为 PEP_DPM_REGISTER_COMPONENT_PERF_STATES，且数据参数指向 PEP_REGISTER_COMPONENT_PERF_STATES 结构。

对于 PEP_DPM_REGISTER_COMPONENT_PERF_STATES 通知，AcceptDeviceNotification 例程始终在调用 IRQL = passive_level 调用。
 
## <a name="pepdpmrequestcomponentperfstate"></a>PEP_DPM_REQUEST_COMPONENT_PERF_STATE 
通知 PEP_DPM_REQUEST_COMPONENT_PERF_STATE 的值。

指向 PEP_REQUEST_COMPONENT_PERF_STATE 结构数据的指针。
Windows 电源管理框架 (PoFx) 的请求的一个或多个性能状态 （P 状态） 更改通知 PEP。

若要发送 PEP_DPM_REQUEST_COMPONENT_PERF_STATE 通知，PoFx 调用 PEP AcceptDeviceNotification 回调例程。 在此调用，通知参数值为 PEP_DPM_REQUEST_COMPONENT_PERF_STATE，且数据参数指向 PEP_REQUEST_COMPONENT_PERF_STATE 结构。

对于 PEP_DPM_REQUEST_COMPONENT_PERF_STATE 通知，AcceptDeviceNotification 例程始终在调用 IRQL = passive_level 调用。
 
## <a name="pepdpmquerycurrentcomponentperfstate"></a>PEP_DPM_QUERY_CURRENT_COMPONENT_PERF_STATE 
通知 PEP_DPM_QUERY_CURRENT_COMPONENT_PERF_STATE 的值。

指向 PEP_QUERY_CURRENT_COMPONENT_PERF_STATE 结构数据的指针。
通知 PEP 它正在查询中指定的 P 状态集的当前 P 状态有关的信息。

若要发送 PEP_DPM_QUERY_CURRENT_COMPONENT_PERF_STATE 通知，PoFx 调用 PEP AcceptDeviceNotification 回调例程。 在此调用，通知参数值为 PEP_DPM_QUERY_CURRENT_COMPONENT_PERF_STATE，且数据参数指向 PEP_QUERY_CURRENT_COMPONENT_PERF_STATE 结构。

对于 PEP_DPM_QUERY_CURRENT_COMPONENT_PERF_STATE 通知，AcceptDeviceNotification 例程始终在调用 IRQL = passive_level 调用。
 
## <a name="pepdpmquerydebuggertransitionrequirements"></a>PEP_DPM_QUERY_DEBUGGER_TRANSITION_REQUIREMENTS 
通知 PEP_DPM_QUERY_DEBUGGER_TRANSITION_REQUIREMENTS 的值。

指向 PEP_DEBUGGER_TRANSITION_REQUIREMENTS 结构数据的指针。
若要查询的组协调或平台状态的发送到 PEP 需要调试器关机。

Windows 电源管理框架 (PoFx) 将此通知发送到查询的一套 PEP 协调或平台状态需要调试器关机。 如果接受此通知，则操作系统将执行所有调试器 power 转换对于 PEP 和 PEP 可能不使用 TransitionCriticalResource 电源管理调试器。 

PEP 已接受的 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 或 PEP_NOTIFY_PPM_QUERY_COORDINATED_STATES 通知后，此通知是发送到调试器中的每个设备。 

若要发送 PEP_DPM_QUERY_DEBUGGER_TRANSITION_REQUIREMENTS 通知，PoFx 调用 PEP AcceptDeviceNotification 回调例程。 对于此类通知，AcceptDeviceNotification 例程将始终调用在 IRQL = DISPATCH_LEVEL。
 
## <a name="pepdpmlowpowerepoch"></a>PEP_DPM_LOW_POWER_EPOCH 
通知 PEP_DPM_LOW_POWER_EPOCH 的值。

指向 PEP_LOW_POWER_EPOCH 结构数据的指针。
此通知已弃用。 
 
## <a name="pepdpmquerysocsubsystem"></a>PEP_DPM_QUERY_SOC_SUBSYSTEM 
通知 PEP_DPM_QUERY_SOC_SUBSYSTEM 的值。

指向 PEP_QUERY_SOC_SUBSYSTEM 结构数据的指针。
发送到 PEP 芯片 (SoC) 子系统上收集有关特定系统的基本信息。

为了收集有关特定 SoC 子系统的基本信息初始化平台空闲状态后，Windows 电源管理框架 (PoFx) 会将此通知发送到 PEP。 PEP 不实现 SoC 子系统记帐或不指定的平台空闲状态时，实现它，则返回 FALSE。 这会指示 OS 停止诊断通知发送到此平台在空闲状态 PEP。

系统的 SubsystemCount 和子系统的 MetadataCount 可以更改与 PEP/BSP 更新。 每次操作系统启动时，可以更改 SubsystemIndex。 

重要 PEP 不能忽略此通知。 PEP 收到此通知因为它对具有非零值 SubsystemCount 此 PlatformIdleStateIndex PEP_DPM_QUERY_SOC_SUBSYSTEM_COUNT 通知做出响应。
 
若要发送 PEP_DPM_QUERY_SOC_SUBSYSTEM 通知，PoFx PEP AcceptDeviceNotification 回调例程在调用 IRQL < DISPATCH_LEVEL。
 
## <a name="pepdpmquerysocsubsystemblockingtime"></a>PEP_DPM_QUERY_SOC_SUBSYSTEM_BLOCKING_TIME 
通知 PEP_DPM_QUERY_SOC_SUBSYSTEM_BLOCKING_TIME 的值。

指向 PEP_QUERY_SOC_SUBSYSTEM_BLOCKING_TIME 结构数据的指针。
OS 想要收集的时间选票总数时，发送到 PEP 芯片 (SoC) 子系统上的特定系统已阻止进入 OS 的不知情的情况下更特定平台的空闲状态。

通常操作系统会调用此扩展已连接备用会话结束时通知操作系统尝试输入指定的平台空闲状态。 PEP_QUERY_SOC_SUBSYSTEM_COUNT。SubsystemCount 值，之前填充 pep 子组件在初始化期间，指定一次多少 PEP_DPM_QUERY_SOC_SUBSYSTEM_BLOCKING_TIME 通知发送到 PEP。 PEP 可以接收给定子系统的多个 PEP_DPM_QUERY_SOC_SUBSYSTEM_BLOCKING_TIME 的通知。 这些通知可能或可能不会使用 PEP_DPM_RESET_SOC_SUBSYSTEM_ACCOUNTING 通知交错。

重要 PEP 不能忽略此通知。 PEP 收到此通知因为它对具有非零值 SubsystemCount 此 PlatformIdleStateIndex PEP_DPM_QUERY_SOC_SUBSYSTEM_COUNT 通知做出响应。
 
若要发送 PEP_DPM_QUERY_SOC_SUBSYSTEM_BLOCKING_TIME 通知，PoFx PEP AcceptDeviceNotification 回调例程在调用 IRQL < DISPATCH_LEVEL。

 
## <a name="pepdpmquerysocsubsystemcount"></a>PEP_DPM_QUERY_SOC_SUBSYSTEM_COUNT 
通知 PEP_DPM_QUERY_SOC_SUBSYSTEM_COUNT 的值。

指向 PEP_QUERY_SOC_SUBSYSTEM_COUNT 结构数据的指针。
初始化后平台空闲状态以告知 OS 是否 PEP 是支持在给定的平台空闲状态芯片 (SoC) 子系统记帐系统，则发送到 PEP。 

这是第一次的 SoC 子系统诊断通知发送到 PEP。 PEP 不实现 SoC 子系统记帐或不指定的平台空闲状态时，实现它返回 FALSE，这种情况下操作系统不会发送 PEP 任何更多 SoC 子系统诊断通知此平台在空闲状态。


请注意 PEP 可以忽略此通知，如果它未实现指定的平台空闲状态的 SoC 诊断通知。
 

若要发送 PEP_DPM_QUERY_SOC_SUBSYSTEM_COUNT 通知，PoFx PEP AcceptDeviceNotification 回调例程在调用 IRQL < DISPATCH_LEVEL。

 
## <a name="pepdpmquerysocsubsystemmetadata"></a>PEP_DPM_QUERY_SOC_SUBSYSTEM_METADATA 
通知 PEP_DPM_QUERY_SOC_SUBSYSTEM_METADATA 的值。

指向 PEP_QUERY_SOC_SUBSYSTEM_METADATA 结构数据的指针。
发送到 PEP 来收集有关其阻塞的时间只是被查询的子系统的可选元数据。

此通知通常发送到 PEP 紧跟 PEP_DPM_QUERY_SOC_SUBSYSTEM_BLOCKING_TIME 通知。 一个 PEP_DPM_QUERY_SOC_SUBSYSTEM_METADATA 通知收集描述子系统的所有元数据键-值对。

重要 PEP 不能忽略此通知。 PEP 收到此通知因为它对具有非零值 SubsystemCount 此 PlatformIdleStateIndex PEP_DPM_QUERY_SOC_SUBSYSTEM_COUNT 通知做出响应。
 
若要发送 PEP_DPM_QUERY_SOC_SUBSYSTEM_METADATA 通知，PoFx 调用 PEP AcceptDeviceNotification 回调例程。 有关此通知，请在 IRQL 调用 AcceptDeviceNotification 例程 < DISPATCH_LEVEL。
 
## <a name="pepdpmresetsocsubsystemaccounting"></a>PEP_DPM_RESET_SOC_SUBSYSTEM_ACCOUNTING 
通知 PEP_DPM_RESET_SOC_SUBSYSTEM_ACCOUNTING 的值。

数据： 指向 PEP_RESET_SOC_SUBSYSTEM_ACCOUNTING 结构的指针。 结构。
发送到 PEP 来清除所有阻塞时间和元数据核算的子系统，执行任何其他初始化所需，并重新启动记帐。 

Windows 电源管理框架 (PoFx) 将此通知发送到 PEP 随时后所有子系统都初始化与操作系统。 通常情况下，此通知时，调用操作系统开始分析围绕什么保持系统的芯片 (SoC) 上的新时间超出指定的平台空闲状态 （面向 DRIPS 在进入连接的待机）。 OS 仅发送此通知的平台为其 PEP 初始化一个或多个 SoC 子系统的空闲状态。

若要发送 PEP_DPM_RESET_SOC_SUBSYSTEM_ACCOUNTING 通知，PoFx PEP AcceptDeviceNotification 回调例程在调用 IRQL < DISPATCH_LEVEL。
 
