---
title: 处理控制请求
description: 处理控制请求
ms.assetid: D2096548-E3E2-4EB6-B3F2-C5AF45E8F4D5
keywords:
- NetAdapterCx 处理控制请求，NetCx 处理控制请求
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: e30d1259789909aeb36206ed2b2880e167e93523
ms.sourcegitcommit: 1600bbad585647840839a6f66078c961c337c268
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2020
ms.locfileid: "88203668"
---
# <a name="handling-control-requests"></a>处理控制请求

在 NetAdapterCx 模型中，客户端驱动程序接收作为 NETREQUEST 对象的大多数控制请求，其中每个对象都表示 (对象标识符) 请求的 OID。 客户端驱动程序通常设置一个或两个 WDF 队列 (称为 NETREQUESTQUEUEs) 来管理控制请求。

NETREQUESTQUEUE 对象是它管理的每个 NETREQUEST 的父对象。 由于队列是 GET-NETADAPTER 对象的子级，因此在删除适配器时，WDF 会自动删除每个队列和任何关联的请求。

若要查看 NetAdapterCx 的所有默认父子关系，请参阅 [NetAdapterCx 对象的摘要](summary-of-netadaptercx-objects.md)。

## <a name="creating-queue-objects"></a>创建队列对象

在 NetAdapterCx 模型中，客户端可以使用两种类型的队列来处理 (Oid) 的控制请求：
*  (Oid) 的常规请求的顺序队列。 NetAdapterCx 每次向客户端传递一次请求。
*  (Oid) 的直接请求的并行队列。 NetAdapterCx 以并行方式传递请求。

有关这些调度方法的详细信息，请参阅 [调度 I/o 请求的方法](../wdf/dispatching-methods-for-i-o-requests.md)。

调用以下方法来创建队列：

* [**NET_REQUEST_QUEUE_CONFIG_INIT_DEFAULT_SEQUENTIAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nf-netrequestqueue-net_request_queue_config_init_default_sequential)
* [**NET_REQUEST_QUEUE_CONFIG_INIT_DEFAULT_PARALLEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nf-netrequestqueue-net_request_queue_config_init_default_parallel)

## <a name="registering-handlers"></a>注册处理程序

对于三个主请求类型 (查询数据、设置数据和方法) ，客户端驱动程序可以提供单个默认处理程序，或者一个或多个特定于 OID 的处理程序。

您可以在同一驱动程序中使用这两种方法，为某些 Oid 提供自定义处理程序，同时将默认处理程序与用于剩余的 switch 语句一起使用。

客户端驱动程序在其 [*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 例程中注册 OID 处理程序。

下面是客户端可以提供的控制请求处理程序：

* [*EVT_NET_REQUEST_METHOD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nc-netrequestqueue-evt_net_request_method)
* [*EVT_NET_REQUEST_QUERY_DATA*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nc-netrequestqueue-evt_net_request_query_data)
* [*EVT_NET_REQUEST_SET_DATA*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nc-netrequestqueue-evt_net_request_set_data)
* [*EVT_NET_REQUEST_DEFAULT_METHOD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nc-netrequestqueue-evt_net_request_default_method)
* [*EVT_NET_REQUEST_DEFAULT_QUERY_DATA*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nc-netrequestqueue-evt_net_request_default_query_data)
* [*EVT_NET_REQUEST_DEFAULT_SET_DATA*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nc-netrequestqueue-evt_net_request_default_set_data)

对于这三种主要请求类型，特定于 OID 的处理程序优先于默认处理程序。 如果客户端不提供指定的 OID，则 NetAdapterCx 将无法请求。

对于除查询数据、设置数据和方法之外的类型的请求，客户端驱动程序可以提供 [*EVT_NET_REQUEST_DEFAULT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nc-netrequestqueue-evt_net_request_default) 事件回调函数。

例如，如果协议驱动程序使用发出 OID 请求，则 `NDIS_REQUEST_TYPE = NdisRequestGeneric1` NetAdapterCx 调用 [*EVT_NET_REQUEST_DEFAULT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nc-netrequestqueue-evt_net_request_default)。 如果客户端驱动程序未提供此类处理程序，NetAdapterCx 将会失败。

下图显示了典型的流：

<img src="images/netcx-adapter-request-handling-flow.png" alt="NetAdapterCx request handling flow" title="NetAdapterCx 请求处理流" style="width: 800px;"/>

以下代码片段演示了客户端如何设置默认处理程序：

```C++
NTSTATUS status;
NET_REQUEST_QUEUE_CONFIG config;
NETREQUESTQUEUE requestQueue;

NET_REQUEST_QUEUE_CONFIG_INIT_DEFAULT_SEQUENTIAL(&config, NetAdapter);
config.EvtRequestDefaultQueryData = MyDefaultQueryData;
config.EvtRequestDefaultSetData = MyDefaultSetData;
config.EvtRequestDefaultMethod = MyDefaultMethod;

config.EvtRequestDefault = MyDefault;
```

若要添加 OID 特定的处理程序，请使用以下方法：

* [**NET_REQUEST_QUEUE_CONFIG_ADD_QUERY_DATA_HANDLER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nf-netrequestqueue-net_request_queue_config_add_query_data_handler)
* [**NET_REQUEST_QUEUE_CONFIG_ADD_SET_DATA_HANDLER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nf-netrequestqueue-net_request_queue_config_add_set_data_handler)
* [**NET_REQUEST_QUEUE_CONFIG_ADD_METHOD_HANDLER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nf-netrequestqueue-net_request_queue_config_add_method_handler)

下面的示例使用指向客户端[*EVT_NET_REQUEST_QUERY_DATA*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nc-netrequestqueue-evt_net_request_query_data)事件回调函数的指针调用[**NET_REQUEST_QUEUE_CONFIG_ADD_QUERY_DATA_HANDLER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nf-netrequestqueue-net_request_queue_config_add_query_data_handler) ，以注册特定 OID 的处理程序：

```C++
NET_REQUEST_QUEUE_CONFIG_ADD_QUERY_DATA_HANDLER(
 &config, OID_GEN_VENDOR_DESCRIPTION,
 EvtQueryGenVendorDescription, sizeof(NIC_VENDOR_DESC));
```

## <a name="creating-the-queue"></a>创建队列

按喜欢的方式设置每个 OID 队列后，调用 [**NetRequestQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nf-netrequestqueue-netrequestqueuecreate) 创建队列：

```C++
status = NetRequestQueueCreate(&config, WDF_NO_OBJECT_ATTRIBUTES, NULL);

if(!NT_SUCCESS(status))
{
 return status;
}
```

NetAdapterCx 可以在 [*EVT_WDF_DEVICE_PREPARE_HARDWARE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 返回 [*EVT_WDF_DEVICE_RELEASE_HARDWARE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)之前立即调用客户端驱动程序的控制请求处理程序。

## <a name="completing-requests"></a>完成请求

客户端驱动程序必须完成其收到的每个 NETREQUEST。 否则，控制请求将保持挂起状态。 如果无法同步处理请求，客户端驱动程序必须在以后完成挂起的 NETREQUEST。 如果无法完成挂起的请求，则可能会导致客户端驱动程序在设备断电时停止响应。

如果原始请求未包含足够大的缓冲区，请调用 [**NetRequestSetBytesNeeded**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequest/nf-netrequest-netrequestsetbytesneeded)。 若要完成控件请求并仅指定完成状态，请从 OID 处理程序中调用 [**NetRequestCompleteWithoutInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequest/nf-netrequest-netrequestcompletewithoutinformation) ，如以下代码片段所示：
 
```C++
 NetRequestCompleteWithoutInformation(Request, STATUS_SUCCESS);
```

如果原始请求包含足够大的缓冲区，则客户端驱动程序将调用 [**NetRequestRetrieveInputOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequest/nf-netrequest-netrequestretrieveinputoutputbuffer) 来检索输入/输出缓冲区。 然后，客户端将使用以下各项之一传输数据并完成请求，具体取决于请求类型：

* [**NetRequestMethodComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequest/nf-netrequest-netrequestmethodcomplete)
* [**NetRequestQueryDataComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequest/nf-netrequest-netrequestquerydatacomplete)
* [**NetRequestSetDataComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequest/nf-netrequest-netrequestsetdatacomplete)
