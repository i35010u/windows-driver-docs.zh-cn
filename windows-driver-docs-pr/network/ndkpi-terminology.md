---
title: NDKPI 术语
description: NDKPI 文档使用以下术语来描述 NDK 提供者和使用者。
ms.assetid: 740A78B3-B7AD-4A8C-8097-D49B39BC9F47
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68dac8baf832d391abe5a35ec70c9db81c6c8fe7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831890"
---
# <a name="ndkpi-terminology"></a>NDKPI 术语


NDKPI 文档使用以下术语来描述 NDK 提供者和使用者。

-   [提供程序函数](#provider-function)
-   [使用者回调](#consumer-callback)
-   [完成回调](#completion-callback)
-   [事件回调](#event-callback)
-   [父对象](#parent-object)
-   [子对象](#child-object)
-   [前面的对象](#antecedent-object)
-   [后续对象](#successor-object)
-   [终结点](#endpoint)
-   [相关主题](#related-topics)

## <a name="provider-function"></a>提供程序函数


NDK 对象的函数调度表中的 NDKPI 函数。 提供程序函数由 NDK 提供程序实现，由 NDK 使用者调用。 所有提供程序函数都将一个指向其操作的对象的指针作为第一个参数。 此指针类似于中C++的 "this" 指针。 此指针始终由使用者显式传递给提供程序函数。

## <a name="consumer-callback"></a>使用者回调


由 NDK 使用者实现并由 NDK 提供程序调用的 NDKPI 函数。 有2种类型的使用者回调：完成回调和事件回调。

## <a name="completion-callback"></a>完成回调


由 NDK 提供程序调用以通知异步提供程序函数完成的用户回调。 在 NDKPI 1.1 和1.2 中，有3个完成回调：

-   *NdkCloseCompletion* （[*NDK\_FN\_关闭\_完成*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_close_completion)）
-   *NdkCreateCompletion* （[*NDK\_FN\_创建\_完成*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_completion)）
-   *NdkRequestCompletion* （[*NDK\_FN\_请求\_完成*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_request_completion)）

## <a name="event-callback"></a>事件回调


一个使用者回调，该回调可由 NDK 提供程序调用，以指示 NDK 对象上的某些事件，而无需由异步提供程序函数触发。 在 NDKPI 1.1 和1.2 中，有4个事件回调：

-   *NdkCqNotificationCallback* （[*NDK\_FN\_CQ\_通知\_回调*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_cq_notification_callback)）
-   *NdkConnectEventCallback* （[*NDK\_FN\_连接\_事件\_回调*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect_event_callback)）
-   *NdkDisconnectEventCallback* （[*NDK\_FN\_断开\_事件\_回调*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_disconnect_event_callback)）
-   *NdkSrqNotificationCallback* （[*NDK\_FN\_.srq\_通知\_回调*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_srq_notification_callback)）

## <a name="parent-object"></a>父对象


一个 NDK 对象，其函数调度表包含一个或多个*NdkCreate*Xxx * * 提供程序函数以创建其他对象。 在 NDKPI 版本1.1 和1.2 中，有2个父对象：

NDK 适配器对象（[**ndk\_适配器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_adapter)）是的父级：

-   [**NDK\_连接器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_connector)
-   [**NDK\_CQ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_cq)
-   [**NDK\_侦听器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_listener)
-   [ **\_映射的 NDK\_逻辑\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_logical_address_mapping)
-   [**NDK\_PD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_pd)
-   [**NDK\_共享\_终结点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_shared_endpoint)

NDK 保护域（PD）对象（[**ndk\_PD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_pd)）是的父级：

-   [**NDK\_MR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_mr)
-   [**NDK\_MW**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_mw)
-   [**NDK\_QP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp)
-   [**NDK\_.SRQ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_srq)

## <a name="child-object"></a>子对象


一个 NDK 对象，该对象通过在父对象的调度表中调用*NdkCreate*Xxx * * 提供程序函数之一来创建。

## <a name="antecedent-object"></a>前面的对象


其他对象依赖的 NDK 对象，以便提供功能。 前面的对象必须在后续对象之前创建。 请注意，所有父对象都是前面的对象，但反之不成立。

## <a name="successor-object"></a>后续对象


依赖于 antecedent 对象的 NDK 对象。 前面的对象必须在后续对象之前创建。 请注意，所有子对象都是后续对象，但反之不成立。 请注意，在某些情况下，可能需要执行前面的/后续关系，这是可选的，并且可能会推迟到后续创建后的某个时间点。

NDKPI 版本1.1 和1.2 定义了以下前面的任务/后续项关系：除父/子关系外，还包括按定义的前面/后续关系：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">前面</th>
<th align="left">后续</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_cq" data-raw-source="[&lt;strong&gt;NDK_CQ&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_cq)"><strong>NDK_CQ</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp" data-raw-source="[&lt;strong&gt;NDK_QP&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp)"><strong>NDK_QP</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_mr" data-raw-source="[&lt;strong&gt;NDK_MR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_mr)"><strong>NDK_MR</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_mw" data-raw-source="[&lt;strong&gt;NDK_MW&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_mw)"><strong>NDK_MW</strong></a> （请参阅<em>NdkBind</em> （<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_bind" data-raw-source="[&lt;em&gt;NDK_FN_BIND&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_bind)"><em>NDK_FN_BIND</em></a>）。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_srq" data-raw-source="[&lt;strong&gt;NDK_SRQ&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_srq)"><strong>NDK_SRQ</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp" data-raw-source="[&lt;strong&gt;NDK_QP&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp)"><strong>NDK_QP</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp" data-raw-source="[&lt;strong&gt;NDK_QP&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp)"><strong>NDK_QP</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_connector" data-raw-source="[&lt;strong&gt;NDK_CONNECTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_connector)"><strong>NDK_CONNECTOR</strong></a> （请参阅<em>NdkConnect</em> （<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect" data-raw-source="[&lt;em&gt;NDK_FN_CONNECT&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect)"><em>NDK_FN_CONNECT</em></a>） <em>、NdkAccept</em> （<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_accept" data-raw-source="[&lt;em&gt;NDK_FN_ACCEPT&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_accept)"><em>NDK_FN_ACCEPT</em></a>）和<em>NdkConnectWithSharedEndpoint</em> （<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect_with_shared_endpoint" data-raw-source="[&lt;em&gt;NDK_FN_CONNECT_WITH_SHARED_ENDPOINT&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect_with_shared_endpoint)"><em>NDK_FN_CONNECT_WITH_SHARED_ENDPOINT</em></a>）。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_shared_endpoint" data-raw-source="[&lt;strong&gt;NDK_SHARED_ENDPOINT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_shared_endpoint)"><strong>NDK_SHARED_ENDPOINT</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_connector" data-raw-source="[&lt;strong&gt;NDK_CONNECTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_connector)"><strong>NDK_CONNECTOR</strong></a> （请参阅<em>NdkConnectWithSharedEndpoint</em> （<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect_with_shared_endpoint" data-raw-source="[&lt;em&gt;NDK_FN_CONNECT_WITH_SHARED_ENDPOINT&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect_with_shared_endpoint)"><em>NDK_FN_CONNECT_WITH_SHARED_ENDPOINT</em></a>）。）</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_listener" data-raw-source="[&lt;strong&gt;NDK_LISTENER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_listener)"><strong>NDK_LISTENER</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_connector" data-raw-source="[&lt;strong&gt;NDK_CONNECTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_connector)"><strong>NDK_CONNECTOR</strong></a> （请参阅<em>NdkConnectEventCallback</em> （<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect_event_callback" data-raw-source="[&lt;em&gt;NDK_FN_CONNECT_EVENT_CALLBACK&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect_event_callback)"><em>NDK_FN_CONNECT_EVENT_CALLBACK</em></a>）。）</p></td>
</tr>
</tbody>
</table>

 

## <a name="endpoint"></a>endpoint


本地地址和 NetworkDirect 端口号的隐式或显式表示形式，用于标识可在其上启动或接受连接的本地点，例如，10.1.1.1：445：

-   [**NDK\_侦听器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_listener)具有一个隐式终结点（在调用*NdkListen* （[*NDK\_FN\_侦听*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_listen)）时，使用者将指定该终结点。
-   通过调用*NdkConnect*连接的[**ndk\_连接器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_connector)（[*ndk\_FN\_CONNECT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect)）还具有一个隐式终结点。
-   一个[**NDK\_共享\_终结点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_shared_endpoint)表示一个显式终结点。 NDK 使用者直接创建终结点，并通过调用*NdkConnectWithSharedEndpoint* （[*NDK\_FN\_CONNECT\_与\_共享\_终结点*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect_with_shared_endpoint)）来显式地使用它来启动一个或多个连接。

**请注意**  NDK 终结点不同于 NDSPI 版本 1 [**INDENDPOINT**](https://docs.microsoft.com/previous-versions/windows/desktop/cc904370(v=vs.85))接口或 NDSPI 版本 2 **INDQueuePair**接口。

 

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口（NDKPI）](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






