---
title: 处理控制请求
description: 处理控制请求
ms.assetid: D2096548-E3E2-4EB6-B3F2-C5AF45E8F4D5
keywords:
- NetAdapterCx 处理控制请求，处理控件的 NetCx 请求
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: a69a536cee452975b9c0853d4911dcc0232c78b1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372767"
---
# <a name="handling-control-requests"></a>处理控制请求

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

在 NetAdapterCx 模型中，客户端驱动程序接收控制请求最多为 NETREQUEST 对象，其中每个表示 OID （对象标识符） 请求。 客户端驱动程序通常设置了一个或两个 WDF 队列 （称为 NETREQUESTQUEUEs） 来管理控制请求。

NETREQUESTQUEUE 对象是它所管理的每个 NETREQUEST 的父级。 由于队列已 NETADAPTER 对象，WDF 的子级会自动删除每个队列和任何关联的请求时删除该适配器。

若要查看 NetAdapterCx 所有默认父子关系，请参阅[NetAdapterCx 摘要对象](summary-of-netadaptercx-objects.md)。

## <a name="creating-queue-objects"></a>创建队列对象

在 NetAdapterCx 模型中，客户端可以使用两种队列类型，用于处理控件请求 (Oid):
* 正常的请求 (Oid) 的顺序队列。 NetAdapterCx 一次将请求传递到客户端之一。
* 直接请求 (Oid) 的并行队列。 NetAdapterCx 提供并行请求。

有关这些调度方法的详细信息，请参阅[调度 I/O 请求的方法](../wdf/dispatching-methods-for-i-o-requests.md)。

调用这些方法来创建队列：

* [**NET_REQUEST_QUEUE_CONFIG_INIT_DEFAULT_SEQUENTIAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nf-netrequestqueue-net_request_queue_config_init_default_sequential)
* [**NET_REQUEST_QUEUE_CONFIG_INIT_DEFAULT_PARALLEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nf-netrequestqueue-net_request_queue_config_init_default_parallel)

## <a name="registering-handlers"></a>注册处理程序

对于每个三种主要的请求类型 （查询数据、 设置数据和方法），客户端驱动程序可以提供一个默认处理程序或一个或多个特定于 OID 的处理程序。

在相同的驱动程序，可以使用这两种方法使用 switch 语句的其余部分使用默认处理程序时提供的某些 Oid 的自定义处理程序。

客户端驱动程序注册 OID 处理程序在其[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)例程。

下面是该控件可以提供客户端的请求处理程序：

* [*EVT_NET_REQUEST_METHOD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nc-netrequestqueue-evt_net_request_method)
* [*EVT_NET_REQUEST_QUERY_DATA*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nc-netrequestqueue-evt_net_request_query_data)
* [*EVT_NET_REQUEST_SET_DATA*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nc-netrequestqueue-evt_net_request_set_data)
* [*EVT_NET_REQUEST_DEFAULT_METHOD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nc-netrequestqueue-evt_net_request_default_method)
* [*EVT_NET_REQUEST_DEFAULT_QUERY_DATA*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nc-netrequestqueue-evt_net_request_default_query_data)
* [*EVT_NET_REQUEST_DEFAULT_SET_DATA*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nc-netrequestqueue-evt_net_request_default_set_data)

对于每个三种主要的请求类型，特定于 OID 的处理程序优先于默认处理程序。 如果客户端提供了这个给定 OID，NetAdapterCx 使请求失败。

对于查询数据、 设置数据和方法以外的类型的请求，客户端驱动程序可以提供[ *EVT_NET_REQUEST_DEFAULT* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nc-netrequestqueue-evt_net_request_default)事件回调函数。

例如，如果协议驱动程序将发出具有的 OID 请求`NDIS_REQUEST_TYPE = NdisRequestGeneric1`，调用 NetAdapterCx [ *EVT_NET_REQUEST_DEFAULT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nc-netrequestqueue-evt_net_request_default)。 NetAdapterCx 使请求失败，如果客户端驱动程序尚未提供此类处理程序。

下图显示了典型的流程：

<img src="images/netcx-adapter-request-handling-flow.png" alt="NetAdapterCx request handling flow" title="NetAdapterCx 请求处理流" style="width: 800px;"/>

以下代码片段演示如何在客户端设置了默认的处理程序：

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

若要添加特定于 OID 的处理程序，请使用这些方法：

* [**NET_REQUEST_QUEUE_CONFIG_ADD_QUERY_DATA_HANDLER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nf-netrequestqueue-net_request_queue_config_add_query_data_handler)
* [**NET_REQUEST_QUEUE_CONFIG_ADD_SET_DATA_HANDLER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nf-netrequestqueue-net_request_queue_config_add_set_data_handler)
* [**NET_REQUEST_QUEUE_CONFIG_ADD_METHOD_HANDLER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nf-netrequestqueue-net_request_queue_config_add_method_handler)

下面的示例调用[ **NET_REQUEST_QUEUE_CONFIG_ADD_QUERY_DATA_HANDLER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nf-netrequestqueue-net_request_queue_config_add_query_data_handler)用一个指针指向客户端[ *EVT_NET_REQUEST_QUERY_DATA*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nc-netrequestqueue-evt_net_request_query_data)事件注册处理程序的特定 OID 的回调函数：

```C++
NET_REQUEST_QUEUE_CONFIG_ADD_QUERY_DATA_HANDLER(
 &config, OID_GEN_VENDOR_DESCRIPTION,
 EvtQueryGenVendorDescription, sizeof(NIC_VENDOR_DESC));
```

## <a name="creating-the-queue"></a>创建队列

一旦设置了每个 OID 队列你喜欢的方式，调用[ **NetRequestQueueCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nf-netrequestqueue-netrequestqueuecreate)以创建队列：

```C++
status = NetRequestQueueCreate(&config, WDF_NO_OBJECT_ATTRIBUTES, NULL);

if(!NT_SUCCESS(status))
{
 return status;
}
```

NetAdapterCx 可以调用客户端驱动程序的控制请求处理程序就立即[ *EVT_WDF_DEVICE_PREPARE_HARDWARE* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)返回至其调用的时间[ *EVT_WDF_DEVICE_RELEASE_HARDWARE*](https://msdn.microsoft.com/library/windows/hardware/ff540890)。

## <a name="completing-requests"></a>完成请求

客户端驱动程序必须完成它接收的每个 NETREQUEST。 否则，控制请求处于挂起状态。 如果不能以同步方式处理该请求，客户端驱动程序必须在更高版本时完成挂起 NETREQUEST。 若要完成挂起的请求可能导致客户端驱动程序，向下打开设备时停止响应。

如果原始请求不包含缓冲区足够大，则调用[ **NetRequestSetBytesNeeded**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequest/nf-netrequest-netrequestsetbytesneeded)。 若要完成控件请求并指定仅完成状态，调用[ **NetRequestCompleteWithoutInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequest/nf-netrequest-netrequestcompletewithoutinformation) OID 的处理程序，如以下代码片段中所示：
 
```C++
 NetRequestCompleteWithoutInformation(Request, STATUS_SUCCESS);
```

如果原始请求未包含大型足够进行缓冲，客户端驱动程序调用[ **NetRequestRetrieveInputOutputBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequest/nf-netrequest-netrequestretrieveinputoutputbuffer)检索输入/输出缓冲区。 然后客户端将数据传输，并完成请求使用以下命令，具体取决于请求类型之一：

* [**NetRequestMethodComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequest/nf-netrequest-netrequestmethodcomplete)
* [**NetRequestQueryDataComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequest/nf-netrequest-netrequestquerydatacomplete)
* [**NetRequestSetDataComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequest/nf-netrequest-netrequestsetdatacomplete)
