---
title: ACPI 通知
description: PEP AcceptAcpiNotification 回调例程接收每个 ACPI 通知均附带一个通知参数，指示通知的类型和数据参数。
ms.assetid: E4DD4386-8008-463B-B048-DE8E559A7456
keywords:
- AcceptAcpiNotification
ms.date: 01/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 654f80a38ba4ff0a2b4edc60521e3be188185c8f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563870"
---
# <a name="acpi-notifications"></a>ACPI 通知

每个 ACPI 通知回调例程接收 PEP AcceptAcpiNotification 伴随通知参数指示类型的通知，和一个数据参数，它指向的数据结构包含的信息指定的通知类型。

在此调用，通知参数设置为 PEP_NOTIFY_ACPI_XXX 常量值，该值指示通知类型。 数据参数指向与此通知类型相关联的 PEP_ACPI_XXX 结构类型。

使用以下 ACPI 通知 Id AcceptAcpiNotification 回调例程。

|通知 ID |ReplTest1 |关联的结构|
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


## <a name="pepnotifyacpipreparedevice"></a>PEP_NOTIFY_ACPI_PREPARE_DEVICE 

通知：PEP_NOTIFY_ACPI_PREPARE_DEVICE 值。
数据：指向由名称标识设备的 PEP_ACPI_PREPARE_DEVICE 结构的指针。
 
允许 PEP 选择是否提供 ACPI 服务的设备。

当 Windows ACPI 驱动程序设备枚举过程中发现在 ACPI 名称空间中的新设备时，Windows 电源管理框架 (PoFx) 将发送此通知。 此通知发送到 Pep 实现 AcceptAcpiNotification 回调例程。

若要发送 PEP_NOTIFY_ACPI_PREPARE_DEVICE 通知，PoFx 调用 PEP AcceptAcpiNotification 例程。 在此调用，通知参数值为 PEP_NOTIFY_ACPI_PREPARE_DEVICE，且数据参数指向 PEP_ACPI_PREPARE_DEVICE 结构，其中包含的设备的名称。 如果提供此设备的 ACPI 服务已准备好 PEP，PEP 会将此结构的 DeviceAccepted 成员设置为 TRUE。 若要拒绝提供此类服务，PEP 此成员设置为 FALSE。

如果 PEP 指示 （通过设置 DeviceAccepted = TRUE），它已准备好提供设备的 ACPI 服务，PoFx 将响应发送 PEP PEP_NOTIFY_ACPI_REGISTER_DEVICE 通知注册 PEP 是唯一的 ACPI 服务提供程序设备。 PoFx 预期只有一个 PEP 来声明 ACPI 设备服务提供程序的角色。

最佳做法是，不执行任何设备初始化 PEP_NOTIFY_ACPI_PREPARE_DEVICE 通知响应。 相反，直到收到设备 PEP_NOTIFY_ACPI_REGISTER_DEVICE 通知时，或对设备调用 ACPI 控制方法 (例如，_INI) 将推迟此初始化。

对于 PEP_NOTIFY_ACPI_PREPARE_DEVICE 通知，AcceptAcpiNotification 例程始终在调用 IRQL = passive_level 调用。
 
## <a name="pepnotifyacpiabandondevice"></a>PEP_NOTIFY_ACPI_ABANDON_DEVICE 

通知：PEP_NOTIFY_ACPI_ABANDON_DEVICE 值。

数据：指向标识已放弃的设备的 PEP_ACPI_ABANDON_DEVICE 结构的指针。
 
指定的设备已被放弃，且不再需要来自 PEP ACPI 服务通知 PEP。

Windows 电源管理框架 (PoFx) 将发送此通知来通知设备不再由操作系统使用 PEP。 PEP 可以使用此通知以清理它已经分配了跟踪设备状态的任何内部存储。

若要发送 PEP_NOTIFY_ACPI_ABANDON_DEVICE 通知，PoFx 调用 PEP AcceptAcpiNotification 回调例程。 在此调用，通知参数值为 PEP_NOTIFY_ACPI_ABANDON_DEVICE，且数据参数指向 PEP_ACPI_ABANDON_DEVICE 结构。

PoFx 仅向已选择加入以提供前一次 PEP_NOTIFY_ACPI_PREPARE_DEVICE 通知中的设备的 ACPI 服务 PEP 发送此通知。 PoFx PEP 已注册为提供这些服务在前一次 PEP_NOTIFY_ACPI_REGISTER_DEVICE 通知中的，如果将发送 PEP_NOTIFY_ACPI_UNREGISTER_DEVICE 设备发送通知之前，PEP_NOTIFY_ACPI_ABANDON_DEVICE通知。

对于 PEP_NOTIFY_ACPI_ABANDON_DEVICE 通知，AcceptAcpiNotification 例程始终在调用 IRQL = passive_level 调用。
 
## <a name="pepnotifyacpiregisterdevice"></a>PEP_NOTIFY_ACPI_REGISTER_DEVICE
通知：PEP_NOTIFY_ACPI_REGISTER_DEVICE 值。

数据：指向标识设备的 PEP_ACPI_REGISTER_DEVICE 结构的指针。 在响应此通知，PEP 被应创建有效的 PEPHANDLE 值标识设备，并将此句柄值写入结构。
 
注册 PEP 是指定的设备的 ACPI 服务仅仅是提供程序。

Windows 电源管理框架 (PoFx) 将此通知发送到已指明 PEP — 在前一次 PEP_NOTIFY_ACPI_PREPARE_DEVICE 通知 — 它已准备好提供指定的设备的 ACPI 服务。

若要发送 PEP_NOTIFY_ACPI_REGISTER_DEVICE 通知，PoFx 调用 PEP AcceptAcpiNotification 例程。 在此调用，通知参数值为 PEP_NOTIFY_ACPI_REGISTER_DEVICE，且数据参数指向标识为其提供 ACPI 服务 PEP 的设备的 PEP_ACPI_REGISTER_DEVICE 结构。

对于 PEP_NOTIFY_ACPI_REGISTER_DEVICE 通知，AcceptAcpiNotification 例程始终在调用 IRQL = passive_level 调用。
 
## <a name="pepnotifyacpiunregisterdevice"></a>PEP_NOTIFY_ACPI_UNREGISTER_DEVICE 

通知：PEP_NOTIFY_ACPI_UNREGISTER_DEVICE 值。

数据：指向包含设备 PEPHANDLE PEP_ACPI_UNREGISTER_DEVICE 结构的指针。
 
取消从 PEP ACPI 服务指定的设备的注册。

在响应此通知，PEP 可能会破坏 PEP 中前一次 PEP_NOTIFY_ACPI_REGISTER_DEVICE 通知此设备创建 PEPHANDLE。

若要发送 PEP_NOTIFY_ACPI_UNREGISTER_DEVICE 通知，PoFx 调用 PEP AcceptAcpiNotification 回调例程。 在此调用，通知参数值为 PEP_NOTIFY_ACPI_UNREGISTER_DEVICE，且数据参数指向 PEP_ACPI_UNREGISTER_DEVICE 结构。

对于 PEP_NOTIFY_ACPI_UNREGISTER_DEVICE 通知，AcceptAcpiNotification 例程始终在调用 IRQL = passive_level 调用。
 
## <a name="pepnotifyacpienumeratedevicenamespace"></a>PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE 

通知：PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE 值。

数据：指向包含的设备的 ACPI 命名空间中对象的枚举的 PEP_ACPI_ENUMERATE_DEVICE_NAMESPACE 结构的指针。
 
查询有关支持在 ACPI 名称空间中指定的设备 PEP 的 ACPI 对象 （本机方法） 的列表 PEP。

Windows ACPI 驱动程序使用此通知枚举的对象生成指定的设备的命名空间。 此后，如果引用到此设备，ACPI 驱动程序将查询仅适用于这些对象 PEP。

发现设备和 PEP 注册以提供设备的 ACPI 服务后不久，Windows 电源管理框架 (PoFx) 将发送 PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE 通知。 有关此注册的详细信息，请参阅 PEP_NOTIFY_ACPI_REGISTER_DEVICE。

若要发送 PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE 通知，PoFx 调用 PEP AcceptAcpiNotification 回调例程。 在此调用，通知参数值为 PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE，且数据参数指向 PEP_ACPI_ENUMERATE_DEVICE_NAMESPACE 结构。

AcceptAcpiNotification 例程应以处理 PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE 通知，并返回 TRUE。 如果不这样做会导致的 bug 检查。

对于 PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE 通知，AcceptAcpiNotification 例程始终在调用 IRQL = passive_level 调用。
 
## <a name="pepnotifyacpiqueryobjectinformation"></a>PEP_NOTIFY_ACPI_QUERY_OBJECT_INFORMATION 

通知：PEP_NOTIFY_ACPI_QUERY_OBJECT_INFORMATION 值。

数据：指向 PEP_ACPI_QUERY_OBJECT_INFORMATION 结构，它指定 ACPI 对象的属性的指针。

查询有关以前枚举 ACPI 对象信息 PEP。

Windows 电源管理框架 (PoFx) 将发送此通知以查询的前一次 PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE 通知在处理期间枚举的对象属性 PEP。 目前，唯一枚举的对象是控制方法。

若要发送 PEP_NOTIFY_ACPI_QUERY_OBJECT_INFORMATION 通知，PoFx 调用 PEP AcceptAcpiNotification 回调例程。 在此调用，通知参数值为 PEP_NOTIFY_ACPI_QUERY_OBJECT_INFORMATION，且数据参数指向 PEP_ACPI_QUERY_OBJECT_INFORMATION 结构。

对于 PEP_NOTIFY_ACPI_QUERY_OBJECT_INFORMATION 通知，AcceptAcpiNotification 例程始终在调用 IRQL = passive_level 调用。
 
## <a name="pepnotifyacpievaluatecontrolmethod"></a>PEP_NOTIFY_ACPI_EVALUATE_CONTROL_METHOD 

通知：PEP_NOTIFY_ACPI_EVALUATE_CONTROL_METHOD 值。

数据：指向 PEP_ACPI_EVALUATE_CONTROL_METHOD 结构，它指定要评估，要提供给此方法，并将结果输出缓冲区的输入的参数的 ACPI 控制方法的指针。

用于计算其 PEP 是已注册处理程序的 ACPI 控制方法。

当 Windows ACPI 驱动程序需要对由 PEP 实现 ACPI 控件方法求值时，Windows 电源管理框架 (PoFx) 会将此通知发送到 PEP。

若要发送 PEP_NOTIFY_ACPI_EVALUATE_CONTROL_METHOD 通知，PoFx 调用 PEP AcceptAcpiNotification 回调例程。 在此调用，通知参数值为 PEP_NOTIFY_ACPI_EVALUATE_CONTROL_METHOD，且数据参数指向 PEP_ACPI_EVALUATE_CONTROL_METHOD 结构。

平台设计器可以选择是否让 PEP 或 ACPI 固件句柄特定的 ACPI 控制方法。 PEP 是 ACPI 控制方法的已注册处理程序，如果 PoFx 响应的请求来自 Windows ACPI 驱动程序，用于评估此方法通过将 PEP_NOTIFY_ACPI_EVALUATE_CONTROL_METHOD 通知发送到 PEP。

下面是一组设备 PEP 可以处理的 ACPI 控制方法的示例：

设备标识和配置： _HID，_CID，_UID，_ADR，_CLS，_SUB，_CRS，_PRS，依次类推。 设备电源管理和唤醒： _PS0 通过 _PS3、 _PR0 通过 _PR3、 _DSW，等等。 特定于设备的方法： _DSM 和任何堆栈的特定于设备的控制方法。 对于特殊的设备，如 ACPI 时间和警报的设备，此通知用于评估时间和警报 （_GCP、 _GRT、 _SRT，等） 的方法。 

对于 PEP_NOTIFY_ACPI_EVALUATE_CONTROL_METHOD 通知，AcceptAcpiNotification 例程始终在调用 IRQL = passive_level 调用。
 
## <a name="pepnotifyacpiquerydevicecontrolresources"></a>PEP_NOTIFY_ACPI_QUERY_DEVICE_CONTROL_RESOURCES 

通知：PEP_NOTIFY_ACPI_QUERY_DEVICE_CONTROL_RESOURCES 值。

数据：指向包含 power 资源列表的 PEP_ACPI_QUERY_DEVICE_CONTROL_RESOURCES 结构的指针。
 
查询有关控制电源与设备所需的原始资源的列表 PEP。

在响应此通知，PEP 提供的原始资源所需控制电源与设备的列表。 Windows ACPI 驱动程序需要此列表，以便它可保留电源资源所需的设备，并提供相应的已翻译资源列表到 PEP （通过发送 PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 通知）. 有关详细信息，请参阅 Raw 和转换资源。

若要发送 PEP_NOTIFY_ACPI_QUERY_DEVICE_CONTROL_RESOURCES 通知，Windows 电源管理框架 (PoFx) 调用 PEP AcceptAcpiNotification 回调例程。 在此调用，通知参数值为 PEP_NOTIFY_ACPI_QUERY_DEVICE_CONTROL_RESOURCES，且数据参数指向 PEP_ACPI_QUERY_DEVICE_CONTROL_RESOURCES 结构。

对于 PEP_NOTIFY_ACPI_QUERY_DEVICE_CONTROL_RESOURCES 通知，AcceptAcpiNotification 例程始终在调用 IRQL = passive_level 调用。
 
## <a name="pepnotifyacpitranslateddevicecontrolresources"></a>PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 

通知：PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 值。

数据：指向包含翻译后的资源的列表的 PEP_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 结构的指针。
 
为任何所需的设备的电源控制资源 PEP 提供翻译后的资源的列表。

Windows 电源管理框架 (PoFx) 将发送此通知，如果 PEP 列出对前一次 PEP_NOTIFY_ACPI_QUERY_DEVICE_CONTROL_RESOURCES 通知响应中的任何原始资源。 PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 通知提供了与相应的已翻译资源列表 PEP。 有关详细信息，请参阅 Raw 和转换资源。

若要发送 PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 通知，PoFx 调用 PEP AcceptAcpiNotification 回调例程。 在此调用，通知参数值为 PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES，且数据参数指向 PEP_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 结构。

对于 PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 通知，AcceptAcpiNotification 例程始终在调用 IRQL = passive_level 调用。
 
## <a name="pepnotifyacpiwork"></a>PEP_NOTIFY_ACPI_WORK 

通知：PEP_NOTIFY_ACPI_WORK 值。

数据：指向 PEP_WORK 结构的指针。
 
每次 PEP 调用 RequestWorker 例程以请求从 Windows 电源管理框架 (PoFx) 的工作项后，发送到 PEP。 此通知用于仅限 ACPI 的工作。

PEP 调用 RequestWorker 例程以请求工作项后，通过发送 PEP PEP_NOTIFY_ACPI_WORK 通知进行响应 PoFx。 但是，不发送此通知，直到有足够处理工作项所需的资源 （即，工作线程）。 这样一来，PoFx 保证，PEP 在通知期间将传递给 PoFx 工作请求可能永远不会失败由于资源不足。

在进入时，PEP 应假定 PEP_WORK 结构未初始化。 若要处理此通知，PEP 应设置为指向描述所请求的工作的 PEP 分配 PEP_WORK_INFORMATION 结构 WorkInformation 成员。 此外，PEP 应设置为 TRUE 以确认 PEP 已处理 PEP_NOTIFY_ACPI_WORK 通知并且 WorkInformation 成员指向有效的 PEP_WORK_INFORMATION 结构 PEP_WORK 结构的 NeedWork 成员。 如果 PEP 失败以处理通知，或无法分配 PEP_WORK_INFORMATION 结构，PEP 应 WorkInformation 成员设置为 NULL，并将 NeedWork 成员设置为 FALSE。

对于 PEP_NOTIFY_ACPI_WORK 通知，AcceptAcpiNotification 例程始终在调用 IRQL = passive_level 调用。
 


