---
title: 在驱动程序中支持 WMI 数据块和事件
description: 在驱动程序中支持 WMI 数据块和事件
ms.assetid: a5138413-3ec4-4c61-9f00-6604759532e9
keywords:
- WMI WDK KMDF，数据块
- WMI WDK KMDF 事件
- 读/写 WMI 数据块 WDK KMDF
- 只读 WMI 数据块 WDK KMDF
- 事件 WDK KMDF WMI
- 跟踪 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b61ff8d7148b180071c6452e08e75b2ee851e937
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355924"
---
# <a name="supporting-wmi-data-blocks-and-events-in-your-driver"></a>在驱动程序中支持 WMI 数据块和事件


\[仅适用于 KMDF\]

基于框架的驱动程序通过提供事件的回调函数来支持 WMI 数据块。 驱动程序通过调用对象方法将事件发送到 WMI 客户端支持 WMI 事件。

### <a href="" id="supporting-read-write-wmi-data-blocks"></a> 支持读/写 WMI 数据块

如果 WMI 数据块中的信息是可读和可写的 WMI 客户端，该驱动程序必须提供[ *EvtWmiInstanceQueryInstance* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_query_instance)服务客户端的回调函数读取请求，加上[ *EvtWmiInstanceSetInstance* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_set_instance)或[ *EvtWmiInstanceSetItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_set_item)回调函数 （或两者） 的服务客户端的写入请求。

如果数据块包含驱动程序在客户端的请求时将执行的方法，该驱动程序还必须提供[ *EvtWmiInstanceExecuteMethod* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_execute_method)回调函数。

如果 WMI 数据块是只写的 （即，WMI 客户端可以将信息写入数据块但不能读取的数据块），该驱动程序不提供[ *EvtWmiInstanceQueryInstance* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_query_instance)回调函数。

### <a href="" id="supporting-read-only-wmi-data-blocks"></a> 支持只读 WMI 数据块

如果 WMI 客户端不能修改 WMI 数据块中的信息，该驱动程序不提供[ *EvtWmiInstanceSetInstance* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_set_instance)或[ *EvtWmiInstanceSetItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_set_item)回调函数。 若要支持 WMI 客户端中的数据块的信息的请求，该驱动程序可以执行以下任一操作：

-   提供[ *EvtWmiInstanceQueryInstance* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_query_instance)回调函数以将驱动程序提供的数据复制到 WMI 提供缓冲区。

-   将数据块的信息存储在 WMI 实例对象的[上下文空间](framework-object-context-space.md)，并设置**UseContextForQuery**的实例的成员[ **WDF\_WMI\_实例\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/ns-wdfwmi-_wdf_wmi_instance_config)结构**TRUE**。

如果驱动程序设置**UseContextForQuery**到**TRUE**，框架将实例对象的上下文空间复制到 WMI 提供的缓冲区时 WMI 客户端请求的实例的信息。 否*EvtWmiInstanceXxx*回调所需的驱动程序是否只能运行一个 WMI 实例提供从其对象上下文区域的只读的、 固定长度数据。

如果只读数据块包含驱动程序在客户端的请求时将执行的方法，该驱动程序还可以提供[ *EvtWmiInstanceExecuteMethod* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nc-wdfwmi-evt_wdf_wmi_instance_execute_method)回调函数。

### <a name="supporting-expensive-wmi-data-blocks"></a>支持成本高昂的 WMI 数据块

如果您的驱动程序收集到一个其 WMI 数据块的支持的动态数据量相对较大，驱动程序应执行以下操作：

-   声明要通过设置为"开销大"的数据块**WdfWmiProviderExpensive**中的标志**标志**的 WMI 提供程序对象的成员[ **WDF\_WMI\_提供程序\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/ns-wdfwmi-_wdf_wmi_provider_config)结构。

-   提供[ *EvtWmiProviderFunctionControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nc-wdfwmi-evt_wdf_wmi_provider_function_control)启用和禁用数据收集的数据块或调用的回调函数[ **WdfWmiProviderIsEnabled** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nf-wdfwmi-wdfwmiproviderisenabled)以确定驱动程序是否应启用或禁用数据收集。

如果您的驱动程序设置**WdfWmiProviderExpensive**标志，框架将调用[ *EvtWmiProviderFunctionControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nc-wdfwmi-evt_wdf_wmi_provider_function_control)时向注册 WMI 客户端的回调函数数据块的访问。 回调函数应启用驱动程序的功能来收集数据。 如果所有 WMI 客户端中都删除其登记为数据块，框架将调用*EvtWmiProviderFunctionControl*回调再次函数，该驱动程序可以停止收集数据。

### <a name="supporting-wmi-events"></a>支持 WMI 事件

驱动程序可以使用 WMI 事件通知的异常情况的 WMI 客户端。 （作为日志记录错误的替代方法，您应使用 WMI 事件）。数据项，例如在 WMI 数据块中的托管的对象格式 (.mof) 文件中定义 WMI 事件。

WMI 客户端注册通知的 WMI 事件。 若要将事件发送到已注册的 WMI 客户端，您的驱动程序调用[ **WdfWmiInstanceFireEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nf-wdfwmi-wdfwmiinstancefireevent)方法。 此方法允许根据需要将特定于事件的数据发送到客户端驱动程序。

如果定义的事件的 WMI 数据块还包含 WMI 数据项或方法的项，该驱动程序提供了适当的 WMI 回调函数。 如果数据块定义的事件，但不包含任何数据或方法的项，必须设置您的驱动程序**WdfWmiProviderEventOnly**中的标志**标志**的 WMI 提供程序对象的成员[ **WDF\_WMI\_提供程序\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/ns-wdfwmi-_wdf_wmi_provider_config)结构。

该驱动程序应调用[ **WdfWmiInstanceFireEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nf-wdfwmi-wdfwmiinstancefireevent)才 WMI 客户端已注册的事件通知。 该驱动程序可以确定是否应调用**WdfWmiInstanceFireEvent**通过提供[ *EvtWmiProviderFunctionControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nc-wdfwmi-evt_wdf_wmi_provider_function_control)回调函数或调用[**WdfWmiProviderIsEnabled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nf-wdfwmi-wdfwmiproviderisenabled)。

### <a name="supporting-wmi-event-tracing"></a>支持 WMI 事件跟踪

与其他 WMI 事件相同的方式在.mof 文件中定义跟踪事件。 当您的驱动程序创建的跟踪事件的 WMI 提供程序对象时，它必须设置**WdfWmiProviderTracing**中的标志**标志**的提供程序对象的成员[ **WDF\_WMI\_提供程序\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/ns-wdfwmi-_wdf_wmi_provider_config)结构。

该驱动程序已注册的提供程序实例后，可以调用[ **WdfWmiProviderGetTracingHandle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nf-wdfwmi-wdfwmiprovidergettracinghandle)获取跟踪句柄。 该驱动程序可以使用作为输入的跟踪句柄[ **WmiTraceMessage** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-wmitracemessage)例程。

有关事件跟踪的详细信息，请参阅：

-   [WMI 事件跟踪](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-event-tracing)

-   [WPP 软件跟踪](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)

 

 





