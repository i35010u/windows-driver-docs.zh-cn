---
title: NDKPI 术语
description: NDKPI 文档使用以下术语来描述 NDK 提供程序和使用者。
ms.assetid: 740A78B3-B7AD-4A8C-8097-D49B39BC9F47
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 609cf7e422c81a3d25b8e6f7a5f585116e11bd7b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522485"
---
# <a name="ndkpi-terminology"></a>NDKPI 术语


NDKPI 文档使用以下术语来描述 NDK 提供程序和使用者。

-   [提供程序函数](#provider-function)
-   [使用者回调](#consumer-callback)
-   [完成回调](#completion-callback)
-   [事件回调](#event-callback)
-   [parent object](#parent-object)
-   [子对象](#child-object)
-   [antecedent object](#antecedent-object)
-   [后继对象](#successor-object)
-   [endpoint](#endpoint)
-   [相关的主题](#related-topics)

## <a name="provider-function"></a>提供程序函数


NDK 对象的函数调度表中一个 NDKPI 函数。 提供程序函数由 NDK 提供程序实现，由 NDK 使用者调用。 提供程序的所有函数的第一个参数都有一个指针指向在其上运行的对象。 此指针是类似于 c + + 中的"this"指针。 此指针始终显式传递时由使用者向提供程序函数。

## <a name="consumer-callback"></a>使用者回调


NDKPI 函数所实现的 NDK 使用者，并通过 NDK 提供程序调用。 有两种类型的使用者的回调： 完成回调和事件的回调。

## <a name="completion-callback"></a>完成回调


一个由 NDK 提供程序，以指示已完成的异步提供程序函数调用的使用者回调。 在 NDKPI 1.1 和 1.2 中，有 3 个完成回调：

-   *NdkCloseCompletion* ([*NDK\_FN\_CLOSE\_COMPLETION*](https://msdn.microsoft.com/library/windows/hardware/hh439862))
-   *NdkCreateCompletion* ([*NDK\_FN\_CREATE\_COMPLETION*](https://msdn.microsoft.com/library/windows/hardware/hh439871))
-   *NdkRequestCompletion* ([*NDK\_FN\_REQUEST\_COMPLETION*](https://msdn.microsoft.com/library/windows/hardware/hh439912))

## <a name="event-callback"></a>事件回调


要异步提供程序函数所触发的情况下以异步方式指示 NDK 对象上的某些事件的 NDK 提供程序可以调用一个使用者回调。 在 NDKPI 1.1 和 1.2 中，有 4 个事件的回调：

-   *NdkCqNotificationCallback* ([*NDK\_FN\_CQ\_NOTIFICATION\_CALLBACK*](https://msdn.microsoft.com/library/windows/hardware/hh439870))
-   *NdkConnectEventCallback* ([*NDK\_FN\_CONNECT\_EVENT\_CALLBACK*](https://msdn.microsoft.com/library/windows/hardware/hh439867))
-   *NdkDisconnectEventCallback* ([*NDK\_FN\_DISCONNECT\_EVENT\_CALLBACK*](https://msdn.microsoft.com/library/windows/hardware/hh439886))
-   *NdkSrqNotificationCallback* ([*NDK\_FN\_SRQ\_NOTIFICATION\_CALLBACK*](https://msdn.microsoft.com/library/windows/hardware/hh439915))

## <a name="parent-object"></a>父对象


其中的函数调度表包含一个或多个的 NDK 对象*NdkCreate*Xxx * * 提供程序函数来创建其他对象。 在 NDKPI 1.1 和 1.2 版中，有 2 个父对象：

NDK 适配器对象 ([**NDK\_适配器**](https://msdn.microsoft.com/library/windows/hardware/hh439848)) 的父级：

-   [**NDK\_连接器**](https://msdn.microsoft.com/library/windows/hardware/hh439852)
-   [**NDK\_CQ**](https://msdn.microsoft.com/library/windows/hardware/hh439854)
-   [**NDK\_LISTENER**](https://msdn.microsoft.com/library/windows/hardware/hh439918)
-   [**NDK\_逻辑\_地址\_映射**](https://msdn.microsoft.com/library/windows/hardware/hh439920)
-   [**NDK\_PD**](https://msdn.microsoft.com/library/windows/hardware/hh439931)
-   [**NDK\_SHARED\_ENDPOINT**](https://msdn.microsoft.com/library/windows/hardware/hh439937)

NDK 保护域 (PD) 对象 ([**NDK\_PD**](https://msdn.microsoft.com/library/windows/hardware/hh439931)) 的父级：

-   [**NDK\_MR**](https://msdn.microsoft.com/library/windows/hardware/hh439922)
-   [**NDK\_MW**](https://msdn.microsoft.com/library/windows/hardware/hh439926)
-   [**NDK\_QP**](https://msdn.microsoft.com/library/windows/hardware/hh439933)
-   [**NDK\_SRQ**](https://msdn.microsoft.com/library/windows/hardware/hh439939)

## <a name="child-object"></a>子对象


通过调用之一创建的 NDK 对象*NdkCreate*中父对象的调度表 Xxx * * 提供程序函数。

## <a name="antecedent-object"></a>antecedent 对象


若要提供的功能依赖于另一个对象 NDK 对象。 后继对象之前，必须创建 antecedent 对象。 请注意，所有父对象都是前面的对象，但反之不成立。

## <a name="successor-object"></a>后继对象


NDK 对象依赖于前面的对象。 后继对象之前，必须创建 antecedent 对象。 请注意，所有子对象都是后续任务对象，但反之不成立。 请注意，前面的任务/后续关系可能是必需、 可选的和/或延迟到点在某些情况下在后续版本创建后。

通过 NDKPI 版本 1.1 和 1.2 （除了是根据定义的前面的任务/后续关系的父/子关系） 定义了以下前面的任务/后续关系：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">前面的任务</th>
<th align="left">后续任务</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439854" data-raw-source="[&lt;strong&gt;NDK_CQ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439854)"><strong>NDK_CQ</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439933" data-raw-source="[&lt;strong&gt;NDK_QP&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439933)"><strong>NDK_QP</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439922" data-raw-source="[&lt;strong&gt;NDK_MR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439922)"><strong>NDK_MR</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439926" data-raw-source="[&lt;strong&gt;NDK_MW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439926)"><strong>NDK_MW</strong> </a> (请参阅<em>NdkBind</em> (<a href="https://msdn.microsoft.com/library/windows/hardware/hh439859" data-raw-source="[&lt;em&gt;NDK_FN_BIND&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439859)"><em>NDK_FN_BIND</em></a>)。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439939" data-raw-source="[&lt;strong&gt;NDK_SRQ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439939)"><strong>NDK_SRQ</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439933" data-raw-source="[&lt;strong&gt;NDK_QP&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439933)"><strong>NDK_QP</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439933" data-raw-source="[&lt;strong&gt;NDK_QP&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439933)"><strong>NDK_QP</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439852" data-raw-source="[&lt;strong&gt;NDK_CONNECTOR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439852)"><strong>NDK_CONNECTOR</strong> </a> (请参阅<em>NdkConnect</em> (<a href="https://msdn.microsoft.com/library/windows/hardware/hh439865" data-raw-source="[&lt;em&gt;NDK_FN_CONNECT&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439865)"><em>NDK_FN_CONNECT</em></a>)， <em>NdkAccept</em> (<a href="https://msdn.microsoft.com/library/windows/hardware/hh439857" data-raw-source="[&lt;em&gt;NDK_FN_ACCEPT&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439857)"> <em>NDK_FN_ACCEPT</em></a>)，和<em>NdkConnectWithSharedEndpoint</em> (<a href="https://msdn.microsoft.com/library/windows/hardware/hh439868" data-raw-source="[&lt;em&gt;NDK_FN_CONNECT_WITH_SHARED_ENDPOINT&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439868)"><em>NDK_FN_CONNECT_WITH_SHARED_ENDPOINT</em></a>).)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439937" data-raw-source="[&lt;strong&gt;NDK_SHARED_ENDPOINT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439937)"><strong>NDK_SHARED_ENDPOINT</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439852" data-raw-source="[&lt;strong&gt;NDK_CONNECTOR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439852)"><strong>NDK_CONNECTOR</strong> </a> (请参阅<em>NdkConnectWithSharedEndpoint</em> (<a href="https://msdn.microsoft.com/library/windows/hardware/hh439868" data-raw-source="[&lt;em&gt;NDK_FN_CONNECT_WITH_SHARED_ENDPOINT&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439868)"><em>NDK_FN_CONNECT_WITH_SHARED_ENDPOINT</em></a>)。)</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439918" data-raw-source="[&lt;strong&gt;NDK_LISTENER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439918)"><strong>NDK_LISTENER</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439852" data-raw-source="[&lt;strong&gt;NDK_CONNECTOR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439852)"><strong>NDK_CONNECTOR</strong> </a> (请参阅<em>NdkConnectEventCallback</em> (<a href="https://msdn.microsoft.com/library/windows/hardware/hh439867" data-raw-source="[&lt;em&gt;NDK_FN_CONNECT_EVENT_CALLBACK&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439867)"><em>NDK_FN_CONNECT_EVENT_CALLBACK</em></a>)。)</p></td>
</tr>
</tbody>
</table>

 

## <a name="endpoint"></a>endpoint


隐式或显式表示形式的标识通过该连接可以启动或接受，例如，10.1.1.1:445 本地点的本地地址和网络 NetworkDirect 端口号：

-   [ **NDK\_侦听器**](https://msdn.microsoft.com/library/windows/hardware/hh439918)有一个隐式终结点 (使用者指定调用时*NdkListen* ([*NDK\_FN\_侦听*](https://msdn.microsoft.com/library/windows/hardware/hh439902)))。
-   [ **NDK\_连接器**](https://msdn.microsoft.com/library/windows/hardware/hh439852)的连接通过调用*NdkConnect* ([*NDK\_FN\_CONNECT*](https://msdn.microsoft.com/library/windows/hardware/hh439865)) 还具有一个隐式终结点。
-   [ **NDK\_共享\_终结点**](https://msdn.microsoft.com/library/windows/hardware/hh439937)表示显式终结点。 NDK 使用者直接创建终结点，并显式使用它通过调用启动一个或多个连接*NdkConnectWithSharedEndpoint* ([*NDK\_FN\_连接\_WITH\_共享\_终结点*](https://msdn.microsoft.com/library/windows/hardware/hh439868))。

**请注意**  NDK 终结点不与 NDSPI 版本 1 相同[ **INDEndpoint** ](https://msdn.microsoft.com/library/cc904370)接口或 NDSPI 版本 2 **INDQueuePair**接口。

 

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






