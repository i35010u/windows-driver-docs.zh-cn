---
title: ACPI 通知
description: PEP 的 AcceptAcpiNotification 回调例程收到的每个 ACPI 通知都附带一个通知参数，该参数指示通知的类型和数据参数。
ms.assetid: E4DD4386-8008-463B-B048-DE8E559A7456
keywords:
- AcceptAcpiNotification
ms.date: 01/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: bfa7ac9f057a464ece015cf904d5e4c333cdeeae
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189559"
---
# <a name="acpi-notifications"></a>ACPI 通知

PEP 的 [*AcceptAcpiNotification*](/windows-hardware/drivers/ddi/pepfx/nc-pepfx-pepcallbacknotifyacpi) 回调例程收到的每个 ACPI 通知都附带一个通知参数，该参数指示通知的类型，一个数据参数指向包含指定通知类型信息的数据结构。

在此调用中，通知参数设置为指示通知类型 PEP_NOTIFY_ACPI_XXX 常量值。 数据参数指向与此通知类型相关联的 PEP_ACPI_XXX 结构类型。

AcceptAcpiNotification 回调例程使用以下 ACPI 通知 Id。

|通知 ID |值 |关联的结构|
|---|---|---| 
|PEP_NOTIFY_ACPI_PREPARE_DEVICE| 0x01 |PEP_ACPI_PREPARE_DEVICE| 
|PEP_NOTIFY_ACPI_ABANDON_DEVICE |0x02 |PEP_ACPI_ABANDON_DEVICE |
|PEP_NOTIFY_ACPI_REGISTER_DEVICE |0x03 |PEP_ACPI_REGISTER_DEVICE |
|PEP_NOTIFY_ACPI_UNREGISTER_DEVICE |0x04 |PEP_ACPI_UNREGISTER_DEVICE |
|PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE |0x05 |PEP_ACPI_ENUMERATE_DEVICE_NAMESPACE |
|PEP_NOTIFY_ACPI_QUERY_OBJECT_INFORMATION |0x06 |PEP_ACPI_QUERY_OBJECT_INFORMATION |
|PEP_NOTIFY_ACPI_EVALUATE_CONTROL_METHOD |0x07 |PEP_ACPI_EVALUATE_CONTROL_METHOD |
|PEP_NOTIFY_ACPI_QUERY_DEVICE_CONTROL_RESOURCES |0x08 |PEP_ACPI_QUERY_DEVICE_CONTROL_RESOURCES |
|PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES |0x09 |PEP_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES |


## <a name="pep_notify_acpi_prepare_device"></a>PEP_NOTIFY_ACPI_PREPARE_DEVICE 

通知：值 PEP_NOTIFY_ACPI_PREPARE_DEVICE。
数据：指向按名称标识设备的 PEP_ACPI_PREPARE_DEVICE 结构的指针。
 
允许 PEP 选择是否为设备提供 ACPI 服务。

当 Windows ACPI 驱动程序在设备枚举过程中发现 ACPI 命名空间中的新设备时，Windows 电源管理框架 (PoFx) 发送此通知。 此通知将发送到实现 AcceptAcpiNotification 回调例程的 PEPs。

若要发送 PEP_NOTIFY_ACPI_PREPARE_DEVICE 通知，PoFx 将调用 PEP 的 AcceptAcpiNotification 例程。 在此调用中，通知参数值为 PEP_NOTIFY_ACPI_PREPARE_DEVICE，Data 参数指向包含设备名称的 PEP_ACPI_PREPARE_DEVICE 结构。 如果 PEP 准备为此设备提供 ACPI 服务，则 PEP 将此结构的 DeviceAccepted 成员设置为 TRUE。 要拒绝提供此类服务，PEP 将此成员设置为 FALSE。

如果 PEP 通过设置 DeviceAccepted = TRUE 来指示 () 准备为设备提供 ACPI 服务，则 PoFx 将通过向此通知发送一个 PEP_NOTIFY_ACPI_REGISTER_DEVICE 通知，将 PEP 注册为设备的 ACPI 服务的唯一提供程序来做出响应。 PoFx 只需要一个 PEP 来声明设备的 ACPI 服务提供程序的角色。

作为最佳做法，请不要执行任何设备初始化来响应 PEP_NOTIFY_ACPI_PREPARE_DEVICE 通知。 相反，请推迟此初始化，直到收到设备的 PEP_NOTIFY_ACPI_REGISTER_DEVICE 通知，或 ACPI 控制方法 (例如，_INI 为设备调用) 。

对于 PEP_NOTIFY_ACPI_PREPARE_DEVICE 通知，AcceptAcpiNotification 例程始终调用 IRQL = PASSIVE_LEVEL。
 
## <a name="pep_notify_acpi_abandon_device"></a>PEP_NOTIFY_ACPI_ABANDON_DEVICE 

通知：值 PEP_NOTIFY_ACPI_ABANDON_DEVICE。

数据：指向用于标识放弃的设备的 PEP_ACPI_ABANDON_DEVICE 结构的指针。
 
通知 PEP：指定的设备已被放弃，不再需要 PEP 的 ACPI 服务。

Windows 电源管理框架 (PoFx) 发送此通知以通知 PEP，操作系统不再使用该设备。 PEP 可以使用此通知来清理为跟踪设备状态而分配的任何内部存储。

若要发送 PEP_NOTIFY_ACPI_ABANDON_DEVICE 通知，PoFx 将调用 PEP 的 AcceptAcpiNotification 回调例程。 在此调用中，通知参数值为 PEP_NOTIFY_ACPI_ABANDON_DEVICE，数据参数指向 PEP_ACPI_ABANDON_DEVICE 结构。

PoFx 仅向已选择在上一个 PEP_NOTIFY_ACPI_PREPARE_DEVICE 通知中为设备提供 ACPI 服务的 PEP 发送此通知。 如果 PEP 注册了在上一个 PEP_NOTIFY_ACPI_REGISTER_DEVICE 通知中提供这些服务，则在发送 PEP_NOTIFY_ACPI_ABANDON_DEVICE 通知之前，PoFx 将为设备发送 PEP_NOTIFY_ACPI_UNREGISTER_DEVICE 通知。

对于 PEP_NOTIFY_ACPI_ABANDON_DEVICE 通知，AcceptAcpiNotification 例程始终调用 IRQL = PASSIVE_LEVEL。
 
## <a name="pep_notify_acpi_register_device"></a>PEP_NOTIFY_ACPI_REGISTER_DEVICE
通知：值 PEP_NOTIFY_ACPI_REGISTER_DEVICE。

数据：指向标识设备的 PEP_ACPI_REGISTER_DEVICE 结构的指针。 为响应此通知，PEP 应创建一个有效的 PEPHANDLE 值以标识设备，并将此句柄值写入结构。
 
将 PEP 注册为指定设备的 ACPI 服务的唯一提供程序。

Windows 电源管理框架 (PoFx) 将此通知发送到在以前的 PEP_NOTIFY_ACPI_PREPARE_DEVICE 通知中指出的 PEP，并准备为指定的设备提供 ACPI 服务。

若要发送 PEP_NOTIFY_ACPI_REGISTER_DEVICE 通知，PoFx 将调用 PEP 的 AcceptAcpiNotification 例程。 在此调用中，通知参数值为 PEP_NOTIFY_ACPI_REGISTER_DEVICE，数据参数指向 PEP_ACPI_REGISTER_DEVICE 结构，该结构标识 PEP 为其提供 ACPI 服务的设备。

对于 PEP_NOTIFY_ACPI_REGISTER_DEVICE 通知，AcceptAcpiNotification 例程始终调用 IRQL = PASSIVE_LEVEL。
 
## <a name="pep_notify_acpi_unregister_device"></a>PEP_NOTIFY_ACPI_UNREGISTER_DEVICE 

通知：值 PEP_NOTIFY_ACPI_UNREGISTER_DEVICE。

数据：指向 PEP_ACPI_UNREGISTER_DEVICE 结构的指针，该结构包含设备的 PEPHANDLE。
 
取消从 PEP 注册 ACPI 服务的指定设备。

为响应此通知，PEP 可以销毁上一个 PEP_NOTIFY_ACPI_REGISTER_DEVICE 通知中为此设备创建的 PEPHANDLE。

若要发送 PEP_NOTIFY_ACPI_UNREGISTER_DEVICE 通知，PoFx 将调用 PEP 的 AcceptAcpiNotification 回调例程。 在此调用中，通知参数值为 PEP_NOTIFY_ACPI_UNREGISTER_DEVICE，数据参数指向 PEP_ACPI_UNREGISTER_DEVICE 结构。

对于 PEP_NOTIFY_ACPI_UNREGISTER_DEVICE 通知，AcceptAcpiNotification 例程始终调用 IRQL = PASSIVE_LEVEL。
 
## <a name="pep_notify_acpi_enumerate_device_namespace"></a>PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE 

通知：值 PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE。

数据：指向 PEP_ACPI_ENUMERATE_DEVICE_NAMESPACE 结构的指针，该结构包含设备的 ACPI 命名空间中的对象的枚举。
 
在 ACPI 命名空间中的指定设备下，使用 PEP)  (本机方法列出 ACPI 对象列表。

Windows ACPI 驱动程序使用此通知所枚举的对象为指定的设备生成命名空间。 此后，当提到此设备时，ACPI 驱动程序只会为这些对象查询 PEP。

Windows 电源管理框架 (PoFx) 在发现设备后不久发送 PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE 通知，并且 PEP 注册为设备提供 ACPI 服务。 有关此注册的详细信息，请参阅 PEP_NOTIFY_ACPI_REGISTER_DEVICE。

若要发送 PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE 通知，PoFx 将调用 PEP 的 AcceptAcpiNotification 回调例程。 在此调用中，通知参数值为 PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE，数据参数指向 PEP_ACPI_ENUMERATE_DEVICE_NAMESPACE 结构。

AcceptAcpiNotification 例程应处理 PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE 通知并返回 TRUE。 如果不这样做，会导致 bug 检查。

对于 PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE 通知，AcceptAcpiNotification 例程始终调用 IRQL = PASSIVE_LEVEL。
 
## <a name="pep_notify_acpi_query_object_information"></a>PEP_NOTIFY_ACPI_QUERY_OBJECT_INFORMATION 

通知：值 PEP_NOTIFY_ACPI_QUERY_OBJECT_INFORMATION。

数据：指向指定 ACPI 对象特性的 PEP_ACPI_QUERY_OBJECT_INFORMATION 结构的指针。

查询 PEP 以获取有关以前枚举的 ACPI 对象的信息。

Windows 电源管理框架 (PoFx) 发送此通知，以便在处理以前 PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE 通知期间枚举的对象的属性中查询 PEP。 目前，列举的对象只有控制方法。

若要发送 PEP_NOTIFY_ACPI_QUERY_OBJECT_INFORMATION 通知，PoFx 将调用 PEP 的 AcceptAcpiNotification 回调例程。 在此调用中，通知参数值为 PEP_NOTIFY_ACPI_QUERY_OBJECT_INFORMATION，数据参数指向 PEP_ACPI_QUERY_OBJECT_INFORMATION 结构。

对于 PEP_NOTIFY_ACPI_QUERY_OBJECT_INFORMATION 通知，AcceptAcpiNotification 例程始终调用 IRQL = PASSIVE_LEVEL。
 
## <a name="pep_notify_acpi_evaluate_control_method"></a>PEP_NOTIFY_ACPI_EVALUATE_CONTROL_METHOD 

通知：值 PEP_NOTIFY_ACPI_EVALUATE_CONTROL_METHOD。

数据：指向 PEP_ACPI_EVALUATE_CONTROL_METHOD 结构的指针，该结构指定要评估的 ACPI 控制方法、提供给此方法的输入参数和结果的输出缓冲区。

用于计算一个 ACPI 控制方法，其中 PEP 是注册的处理程序。

当 Windows ACPI 驱动程序需要评估由 PEP 实现的 ACPI 控制方法时，Windows 电源管理框架 (PoFx) 会将此通知发送到 PEP。

若要发送 PEP_NOTIFY_ACPI_EVALUATE_CONTROL_METHOD 通知，PoFx 将调用 PEP 的 AcceptAcpiNotification 回调例程。 在此调用中，通知参数值为 PEP_NOTIFY_ACPI_EVALUATE_CONTROL_METHOD，数据参数指向 PEP_ACPI_EVALUATE_CONTROL_METHOD 结构。

平台设计器可以选择是否让 PEP 或 ACPI 固件处理特定的 ACPI 控制方法。 如果 PEP 是 ACPI 控制方法的注册处理程序，PoFx 将响应来自 Windows ACPI 驱动程序的请求，通过将 PEP_NOTIFY_ACPI_EVALUATE_CONTROL_METHOD 通知发送到 PEP 来评估此方法。

下面列出了 PEP 可为设备处理的 ACPI 控制方法示例：

设备标识和配置： _HID、_CID、_UID、_ADR、_CLS、_SUB、_CRS、_PRS 等。 设备电源管理和唤醒：通过 _PS3 _PS0，_PR0 到 _PR3，_DSW 等。 特定于设备的方法： _DSM 和任何特定于设备堆栈的控制方法。 对于特殊设备，如 ACPI 时间和警报设备，此通知用于评估 (_GCP、_GRT、_SRT 等) 的时间和警报方法。 

对于 PEP_NOTIFY_ACPI_EVALUATE_CONTROL_METHOD 通知，AcceptAcpiNotification 例程始终调用 IRQL = PASSIVE_LEVEL。
 
## <a name="pep_notify_acpi_query_device_control_resources"></a>PEP_NOTIFY_ACPI_QUERY_DEVICE_CONTROL_RESOURCES 

通知：值 PEP_NOTIFY_ACPI_QUERY_DEVICE_CONTROL_RESOURCES。

数据：指向包含电源资源列表的 PEP_ACPI_QUERY_DEVICE_CONTROL_RESOURCES 结构的指针。
 
查询 PEP 以获得控制设备电源所需的原始资源的列表。

为响应此通知，PEP 提供控制设备电源所需的原始资源的列表。 Windows ACPI 驱动程序需要此列表才能保留设备所需的电源资源，并通过发送 PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 通知) 向 PEP (提供相应的已转换资源列表。 有关详细信息，请参阅原始资源和已翻译资源。

若要发送 PEP_NOTIFY_ACPI_QUERY_DEVICE_CONTROL_RESOURCES 通知，Windows 电源管理框架 (PoFx) 调用 PEP 的 AcceptAcpiNotification 回调例程。 在此调用中，通知参数值为 PEP_NOTIFY_ACPI_QUERY_DEVICE_CONTROL_RESOURCES，数据参数指向 PEP_ACPI_QUERY_DEVICE_CONTROL_RESOURCES 结构。

对于 PEP_NOTIFY_ACPI_QUERY_DEVICE_CONTROL_RESOURCES 通知，AcceptAcpiNotification 例程始终调用 IRQL = PASSIVE_LEVEL。
 
## <a name="pep_notify_acpi_translated_device_control_resources"></a>PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 

通知：值 PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES。

数据：指向包含已翻译资源列表的 PEP_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 结构的指针。
 
为 PEP 提供设备所需的任何电源控制资源的已翻译资源列表。

如果 PEP 列出了任何原始资源来响应以前的 PEP_NOTIFY_ACPI_QUERY_DEVICE_CONTROL_RESOURCES 通知，则 Windows 电源管理框架 (PoFx) 将发送此通知。 PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 通知向 PEP 提供相应的已翻译资源列表。 有关详细信息，请参阅原始资源和已翻译资源。

若要发送 PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 通知，PoFx 将调用 PEP 的 AcceptAcpiNotification 回调例程。 在此调用中，通知参数值为 PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES，数据参数指向 PEP_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 结构。

对于 PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 通知，AcceptAcpiNotification 例程始终调用 IRQL = PASSIVE_LEVEL。
 
## <a name="pep_notify_acpi_work"></a>PEP_NOTIFY_ACPI_WORK 

通知：值 PEP_NOTIFY_ACPI_WORK。

数据：指向 PEP_WORK 结构的指针。
 
每次 PEP 调用 RequestWorker 例程来请求 Windows 电源管理框架中的工作项时，都会发送到 PEP (PoFx) 。 此通知仅用于 ACPI 工作。

在 PEP 调用 RequestWorker 例程来请求工作项后，PoFx 将通过向 PEP 发送 PEP_NOTIFY_ACPI_WORK 通知来做出响应。 但是，在 (的资源（) 处理工作项所需的工作线程可用）之前，不会发送此通知。 通过这种方式，PoFx 保证在通知过程中，PEP 传递到 PoFx 的工作请求永远不会因资源不足而失败。

输入时，PEP 应假定 PEP_WORK 结构未初始化。 为了处理此通知，PEP 应将 WorkInformation 成员设置为指向 PEP 分配的 PEP_WORK_INFORMATION 结构，该结构描述正在请求的工作。 此外，PEP 应将 PEP_WORK 结构的 NeedWork 成员设置为 TRUE，以确认 PEP 已处理 PEP_NOTIFY_ACPI_WORK 通知，并且 WorkInformation 成员指向有效的 PEP_WORK_INFORMATION 结构。 如果 PEP 无法处理通知或无法分配 PEP_WORK_INFORMATION 结构，则 PEP 应将 WorkInformation 成员设置为 NULL，并将 NeedWork 成员设置为 FALSE。

对于 PEP_NOTIFY_ACPI_WORK 通知，AcceptAcpiNotification 例程始终调用 IRQL = PASSIVE_LEVEL。
