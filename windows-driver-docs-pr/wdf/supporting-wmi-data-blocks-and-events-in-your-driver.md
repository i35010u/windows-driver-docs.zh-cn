---
title: 在驱动程序中支持 WMI 数据块和事件
description: 在驱动程序中支持 WMI 数据块和事件
keywords:
- WMI WDK KMDF，数据块
- WMI WDK KMDF，事件
- 读/写 WMI 数据块 WDK KMDF
- 只读 WMI 数据块 WDK KMDF
- 事件 WDK KMDF、WMI
- 跟踪 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0348123e89c97231775dafe9f6d6ea5b79185bf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815569"
---
# <a name="supporting-wmi-data-blocks-and-events-in-your-driver"></a>在驱动程序中支持 WMI 数据块和事件


\[仅适用于 KMDF\]

基于框架的驱动程序通过提供事件回调函数支持 WMI 数据块。 驱动程序通过调用向 WMI 客户端发送事件的对象方法支持 WMI 事件。

### <a name="supporting-readwrite-wmi-data-blocks"></a><a href="" id="supporting-read-write-wmi-data-blocks"></a> 支持读/写 WMI 数据块

如果 WMI 数据块中的信息既可由 WMI 客户端读取和写入，则驱动程序必须提供一个 [*EvtWmiInstanceQueryInstance*](/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_query_instance) 回调函数，该函数可为客户端的读取请求提供服务，此外还可以使用 [*EvtWmiInstanceSetInstance*](/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_set_instance) 或 [*EvtWmiInstanceSetItem*](/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_set_item) 回调 (函数来处理客户端写入请求) 。

如果数据块包含驱动程序在客户端请求中执行的方法，则驱动程序还必须提供 [*EvtWmiInstanceExecuteMethod*](/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_execute_method) 回调函数。

如果 WMI 数据块是只写的 (也就是说，WMI 客户端可以将信息写入数据块，但无法读取数据块) ，驱动程序不提供 [*EvtWmiInstanceQueryInstance*](/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_query_instance) 回调函数。

### <a name="supporting-read-only-wmi-data-blocks"></a><a href="" id="supporting-read-only-wmi-data-blocks"></a> 支持 Read-Only WMI 数据块

如果 wmi 客户端无法修改 WMI 数据块中的信息，则该驱动程序不提供 [*EvtWmiInstanceSetInstance*](/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_set_instance) 或 [*EvtWmiInstanceSetItem*](/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_set_item) 回调函数。 若要支持来自 WMI 客户端的数据块信息请求，驱动程序可以执行以下任一操作：

-   提供 [*EvtWmiInstanceQueryInstance*](/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_query_instance) 回调函数以将驱动程序提供的数据复制到 WMI 提供的缓冲区中。

-   将数据块的信息存储在 WMI 实例对象的 [上下文空间](framework-object-context-space.md)中，并将实例的 [**WDF \_ WMI \_ 实例 \_ 配置**](/windows-hardware/drivers/ddi/wdfwmi/ns-wdfwmi-_wdf_wmi_instance_config)结构的 **UseContextForQuery** 成员设置为 **TRUE**。

如果驱动程序将 **UseContextForQuery** 设置为 **TRUE**，则当 wmi 客户端请求实例的信息时，框架会将实例对象的上下文空间复制到 wmi 提供的缓冲区中。 如果驱动程序只有一个通过其对象上下文区域提供只读、固定长度的数据的 WMI 实例，则不需要 *EvtWmiInstanceXxx* 回调。

如果只读数据块包含驱动程序在客户端请求中执行的方法，则驱动程序还可以提供 [*EvtWmiInstanceExecuteMethod*](/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_execute_method) 回调函数。

### <a name="supporting-expensive-wmi-data-blocks"></a>支持昂贵的 WMI 数据块

如果你的驱动程序收集了相对大量的动态数据以支持其 WMI 数据块之一，则驱动程序应执行以下操作：

-   通过设置 WMI 提供程序对象的 [**WDF \_ wmi \_ 提供程序 \_ 配置**](/windows-hardware/drivers/ddi/wdfwmi/ns-wdfwmi-_wdf_wmi_provider_config)结构中 **Flags** 成员的 **WdfWmiProviderExpensive** 标志，将数据块声明为 "昂贵"。

-   提供一个 [*EvtWmiProviderFunctionControl*](/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_provider_function_control) 回调函数，该函数启用和禁用数据块的数据收集，或调用 [**WdfWmiProviderIsEnabled**](/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdfwmiproviderisenabled) 来确定驱动程序是否应启用或禁用数据收集。

如果驱动程序设置了 **WdfWmiProviderExpensive** 标志，则当 WMI 客户端注册访问数据块时，框架将调用 [*EvtWmiProviderFunctionControl*](/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_provider_function_control) 回调函数。 回调函数应启用驱动程序收集数据的能力。 如果所有 WMI 客户端都删除其对数据块的注册，则框架将再次调用 *EvtWmiProviderFunctionControl* 回调函数，以便驱动程序可以停止收集数据。

### <a name="supporting-wmi-events"></a>支持 WMI 事件

驱动程序可以使用 WMI 事件通知 WMI 客户端异常情况。  (不应使用 WMI 事件作为记录错误的替代方法。 ) 与数据项一样，WMI 事件是在托管对象格式 ( mof) 文件中的 WMI 数据块中定义的。

WMI 客户端注册 WMI 事件的通知。 若要将事件发送到已注册的 WMI 客户端，驱动程序将调用 [**WdfWmiInstanceFireEvent**](/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdfwmiinstancefireevent) 方法。 此方法允许驱动程序选择性地将特定于事件的数据发送到客户端。

如果定义事件的 WMI 数据块还包含 WMI 数据项或方法项，则驱动程序将提供相应的 WMI 回调函数。 如果数据块定义了事件但不包含任何数据或方法项，则驱动程序必须在 WMI 提供程序对象的 [**WDF \_ wmi \_ 提供程序 \_ 配置**](/windows-hardware/drivers/ddi/wdfwmi/ns-wdfwmi-_wdf_wmi_provider_config)结构的 **Flags** 成员中设置 **WdfWmiProviderEventOnly** 标志。

仅当 WMI 客户端已注册事件通知时，驱动程序才应调用 [**WdfWmiInstanceFireEvent**](/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdfwmiinstancefireevent) 。 驱动程序可以通过提供 [*EvtWmiProviderFunctionControl*](/windows-hardware/drivers/ddi/wdfwmi/nc-wdfwmi-evt_wdf_wmi_provider_function_control)回调函数或调用 [**WdfWmiProviderIsEnabled**](/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdfwmiproviderisenabled)来确定它是否应调用 **WdfWmiInstanceFireEvent** 。

### <a name="supporting-wmi-event-tracing"></a>支持 WMI 事件跟踪

在 mof 文件中定义跟踪事件的方式与其他 WMI 事件的方式相同。 当驱动程序为跟踪事件创建 WMI 提供程序对象时，它必须在提供程序对象的 [**WDF \_ WMI \_ 提供程序 \_ 配置**](/windows-hardware/drivers/ddi/wdfwmi/ns-wdfwmi-_wdf_wmi_provider_config)结构的 **Flags** 成员中设置 **WdfWmiProviderTracing** 标志。

注册提供程序实例之后，驱动程序可以调用 [**WdfWmiProviderGetTracingHandle**](/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdfwmiprovidergettracinghandle) 来获取跟踪句柄。 驱动程序可以使用跟踪句柄作为 [**WmiTraceMessage**](/windows-hardware/drivers/ddi/wdm/nf-wdm-wmitracemessage) 例程的输入。

有关事件跟踪的详细信息，请参阅：

-   [WMI 事件跟踪](../kernel/wmi-event-tracing.md)

-   [WPP 软件跟踪](../devtest/wpp-software-tracing.md)

 

