---
title: MB 操作语义
description: MB 操作语义
ms.assetid: 5f04b7fd-3df3-4efa-bb26-c7f4cd3c9ebd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2c26d2ec41b6d136864fdb9752af3560e09b9b9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844278"
---
# <a name="mb-operational-semantics"></a>MB 操作语义


### <a name="asynchronous-transactions"></a>异步事务

MB 驱动程序模型通过使用 NDIS 1.x 中提供的异步通知机制，在 MB 服务和微型端口驱动程序之间采用非阻止操作语义。 此机制允许 MB 服务继续将 OID 请求发送到微型端口驱动程序以进行处理，而无需等待当前操作完成。

异步事务是从初始请求开始的三向握手，后跟请求状态响应，然后最后的事务性指示结束。 请求状态响应是临时的，因为它仅确认微型端口驱动程序已收到请求。 跟进异步指示是事务性的，因为它指示事务的完成。 微型端口驱动程序返回状态代码以及事务性指示中的结果数据。

### <a name="asynchronous-set-and-query-requests"></a>异步*集*和*查询*请求

MB 服务使用的许多*设置*和*查询*OID 请求都是异步处理的。 有关*设置*和*查询*OID 请求的详细信息，请参阅[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)。 [MB 数据模型](mb-data-model.md)主题中的 "WWAN 特定的 oid" 表标识了哪些 oid 是异步处理的。

下图表示在 MB 服务和微型端口驱动程序之间的异步*查询*事务的交互顺序。 以粗体显示的标签表示 OID 标识符或事务流控制，而常规文本中的标签表示 OID 结构中的重要标志。

![说明移动宽带服务和微型端口驱动程序之间的异步查询事务的交互顺序的关系图](images/wwanasyncquerytransaction.png)

对于*查询*和*设置*请求，三向握手都是相同的。

除了[OID\_WWAN\_DRIVER\_cap](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-driver-caps)以外，其他所有 MB 特定的 OID 请求都遵循用于微端口驱动程序和 MB 服务之间的信息交换的异步事务机制，还提供以下附加说明：

-   小型端口驱动程序应立即对任何错误条件（如无效的 OID 请求）进行 OID 请求失败。

-   微型端口驱动程序必须返回在事件通知结构的**uStatus**成员中指定了正确错误代码（例如，WWAN\_状态\_XXX）的任何特定于 wwan 的错误条件。 如果需要，微型端口驱动程序还应根据需要在**uStatus**成员后面的成员中进行适当填充。 例如，微型端口驱动程序应填写[**NDIS\_WWAN\_\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_context_state)的**uNwError**成员（如果可用）。 但是，如果在处理与 Pin 相关的 Oid 时出现故障，微型端口驱动程序可能不一定具有要在[**NDIS\_WWAN\_pin\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)的**PinState**成员中指定的当前 PIN 状态信息。

-   小型端口驱动程序应将 NDIS\_状态返回\_指示\_作为所有异步 OID 请求的临时响应需要。

-   微型端口驱动程序应能够区分 OID 请求导致的设备状态更改与其他原因。 小型端口驱动程序应发送由 OID 请求引起的状态更改的事务性通知，并且应从其他原因为状态更改发送未经请求的事件通知。

-   微型端口驱动程序负责管理内核模式内存，不过，MB 服务最初为请求分配内存。 当 MB 服务接收到来自微型端口驱动程序的响应后，该服务可能会释放为 OID 请求分配的用户模式内存。

下图显示了 MB 服务和微型端口驱动程序之间的异步*集*事务的交互顺序。 以粗体显示的标签表示 OID 标识符或事务流控制，而常规文本中的标签表示 OID 结构中的重要标志。

![说明移动宽带服务和微型端口驱动程序之间的异步集事务交互顺序的关系图](images/wwanasyncsettransaction.png)

### <a name="asynchronous-response"></a>异步响应

*Ndis 6.0 规范*（随 Windows Vista 一起发布）引入了新的状态代码，NDIS\_状态\_指示\_需要，对于微型端口驱动程序，将事务的异步性质传达给微型端口驱动程序对 OID 请求的临时响应中的 MB 服务。

如[Mb 接口概述](mb-interface-overview.md)中所述，mb 服务不能直接访问由 mb 微型端口驱动程序分配的内核模式内存。 假定内核模式内存中存储的执行结果被复制并可由某些中介（如 WMI 或[NDIS 筛选器驱动程序](ndis-filter-drivers2.md)）提供给 MB 服务。 因此，小型端口驱动程序可以在事务指示中返回[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)函数调用后释放已分配的内核模式内存。

下面的过程介绍了微型端口驱动程序和 MB 服务必须遵循的握手过程。

### <a name="mb-miniport-driver-procedure"></a>MB 微型端口驱动程序过程

收到 OID 请求后，微型端口驱动程序应执行以下步骤：

1.  在内核模式下分配内存，以复制与 OID 请求关联的[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)数据结构的内容。

2.  在请求的参数中，确保还复制 OID 请求结构的**RequestId**和**RequestHandle**成员。 稍后将在事务*指示*中使用这些成员。

3.  返回临时 NDIS\_状态\_指示\_所需状态响应，以通知 MB 服务微型端口驱动程序将异步完成请求。

4.  完成操作后，根据需要将结果存储在本地或驱动程序分配的内存中。

5.  调用[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)函数以通知 MB 服务，未完成的操作已完成。 小型端口驱动程序应填写 NDIS\_状态\_指示结构的成员，如下所示：
    1.  将**StatusCode**成员设置为状态通知的类型。 例如，NDIS\_状态\_WWAN\_XXX。
    2.  将**DestinationHandle**成员设置为在微型端口驱动程序收到相应 OID 请求时在 NDIS\_OID\_请求数据结构中收到的**RequestHandle**成员。
    3.  设置**RequestId**成员，使其在微型端口驱动程序收到相应的 OID 请求时，与 NDIS\_OID 的**RequestId**成员匹配\_请求状态结构。
    4.  将**StatusBuffer**和**StatusBufferSize**成员设置为分别指向微型端口驱动程序分配的内存和内存缓冲区的大小。 此内存缓冲区包含已完成操作的结果。
    5.  如果操作成功完成，请将**uStatus**成员设置为 WWAN\_状态\_SUCCESS。 否则，请将**uStatus**成员设置为相应的 WWAN\_状态\_XXX 值以指示失败的类型。

6.  当函数调用返回时，微型端口驱动程序应释放为 OID 请求分配的内存。

### <a name="mb-service-procedure"></a>MB 服务过程

MB 服务使用以下过程处理异步事务：

1.  基于 OID 数据结构为请求分配缓冲区内存。 用适当的值填充数据结构成员。

2.  调用[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)函数，并将**INFORMATIONBUFFER**成员指向 oid 请求的 oid 数据结构，并等待微型端口驱动程序做出响应。

3.  收到 NDIS\_状态\_指示\_需要来自微型端口驱动程序的临时响应时，MB 服务将保存**RequestId**，释放已分配的内存，然后将事务标记为打开。 此时，MB 服务可以自由处理后续 OID 请求和通知。

4.  收到具有 NDIS\_状态的通知\_WWAN\_XXX 作为**StatusCode**值时，请检查 RequestId 是否与标记为打开的任何事务的**RequestId**匹配。 如果有匹配项，服务将关闭该事务。 如果未找到匹配项，则将通知视为未经请求的事件通知。

5.  处理**StatusBuffer**成员中返回的数据，并根据需要对 MB 服务进行状态更改。

### <a name="indications"></a>亮起

微型端口驱动程序可以生成两种类型的 WWAN 特定*迹象*：

-   在 MB 设备中因对象状态发生更改而导致的事件通知。

-   通知异步操作完成的事务性通知。

在这两种情况下，微型端口驱动程序都应调用 NdisMIndicateStatusEx 函数。

### <a name="event-notification"></a>事件通知

事件通知未经许可，因为微型端口驱动程序将指示作为状态更改事件主动发送到 MB 服务。 状态更改是由除 MB 服务以外的其他实体中的操作引起的。 MB 服务假定微型端口驱动程序能够检测到发生更改的原因。

对于任何特定于 WWAN 的事件通知，微型端口驱动程序必须将 NDIS\_状态\_指示结构的**RequestId**成员设置为零。 **StatusCode**成员指定 MB 设备中已更改的对象。 微型端口驱动程序可以将此对象设置为以下任何值：

[ **\_WWAN\_设备\_CAP 的 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps)

[**NDIS\_状态\_WWAN\_就绪\_信息**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ready-info)

[ **\_WWAN\_无线电\_状态的 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-radio-state)

[ **\_WWAN\_PIN\_信息的 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-info)

[ **\_WWAN\_PIN\_列表的 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-list)

[**WWAN\_HOME\_提供程序\_的 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider)

[ **\_WWAN\_首选\_提供程序的 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-providers)

[ **\_WWAN\_可见\_提供程序的 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers)

[**WWAN\_REGISTER\_状态\_NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-register-state)

[**WWAN\_数据包\_服务\_的 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service)

[**NDIS\_状态\_WWAN\_信号\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-signal-state)

[ **\_WWAN\_上下文\_状态的 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-context-state)

[ **\_WWAN\_预配\_上下文的 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-provisioned-contexts)

[ **\_WWAN\_服务\_激活的 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-service-activation)

[**WWAN\_SMS\_配置\_的 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-configuration)

[ **\_WWAN\_SMS\_接收的 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-receive)

[**WWAN\_SMS\_发送\_的 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-send)

[ **\_WWAN\_SMS\_删除的 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-delete)

[ **\_WWAN\_SMS\_状态的 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-status)

[ **\_WWAN\_供应商\_特定的 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-vendor-specific)

MB 服务还可以处理 NDIS 发出的其他事件通知。 这些非 MB 事件通知不必遵守其**RequestId**值设置为零的要求。

### <a name="transactional-notifications"></a>事务性通知

微型端口驱动程序使用事务性通知来通知 MB 服务异步事务已完成，MB 服务使用事务性通知来关闭打开的事务，并更新其状态机。

MB 服务需要事务性通知，以便它可以关闭打开的事务。 它是异步事务中的 MB 服务和微型端口驱动程序之间的三向握手的最终交换。 任何事务通知中 NDIS\_状态\_指示的**RequestId**成员的值都必须为非零值，该值从同一事务中的相应请求中复制。

要使异步机制正常运行，必须正确地将 NDIS\_状态\_指示结构的**RequestId**成员设置为。 MB 服务确保**RequestId**值在所有未完成的请求中是唯一的，非零。 小型端口驱动程序必须在相应的*指示*中返回相同的**RequestId**值，以便 MB 服务将指示与打开的事务关联起来。

### <a name="status-indication-structure"></a>状态指示结构

给定 OID 请求和未经请求的事件通知结构的异步响应会将*StatusIndication*参数的**StatusBuffer**成员指向的以下结构成员共享到[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)：

```C++
typedef struct _NDIS_WWAN_XXX {
  NDIS_OBJECT_HEADER Header;
  WWAN_STATUS uStatus;
  ULONG uNwError;//Optional. Only used for network operations.
  WWAN_XXX XxxStruct;
} NDIS_WWAN_XXX, *PNDIS_WWAN_XXX;
```

如果 NDIS\_状态\_指示结构的**RequestId**成员的值为零，则表示它是一个未经请求的事件通知，并可随时发生。

如果任何*set*或*query* OID 请求的返回指示中的**uStatus**成员不等于 wwan\_状态\_成功，关联 NDIS\_WWAN\_XXX 结构的成员不需要有效。

如果基于网络事件的未经请求的事件通知，微型端口驱动程序必须根据需要填写**uNwError**成员（如果适用）。

下表显示了在基于 GSM 的网络的*3GPP TS 24.008 规范*中定义的注册、数据包附加和数据包分离原因：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">3GPP 24.008 原因代码</th>
<th align="left">原因代码的解释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>2-HLR 中未知的国际移动用户标识（IMSI）</p></td>
<td align="left"><p>SIM 或设备未激活，或订阅已过期，导致网络停用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4-IMSI 在 VLR 中未知</p></td>
<td align="left"><p>漫游功能未订阅。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6-非法</p></td>
<td align="left"><p>由于报告被盗，网络阻止了 MS。</p></td>
</tr>
<tr class="even">
<td align="left"><p>7-不允许 GPRS 服务</p></td>
<td align="left"><p>用户没有 GPRS 订阅。 用户只有一个语音连接订阅。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>不允许使用 8-GPRS 和非 GPRS 服务</p></td>
<td align="left"><p>不允许 GPRS 和非 GPRS 服务。</p></td>
</tr>
<tr class="even">
<td align="left"><p>11-不允许 PLMN</p></td>
<td align="left"><p>由于订阅过期或其他原因，服务被网络阻止。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>12-不允许使用位置区域</p></td>
<td align="left"><p>用户订阅不允许在 "当前位置" 区域访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p>13-此位置区域不允许漫游</p></td>
<td align="left"><p>该订阅允许漫游，但不允许漫游。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>14-此 PLMN 中不允许使用 GPRS 服务</p></td>
<td align="left"><p>选定的网络提供程序不会向 MS 提供 GPRS 服务。</p></td>
</tr>
<tr class="even">
<td align="left"><p>15-位置区域中没有合适的单元格</p></td>
<td align="left"><p>服务没有订阅。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>17-网络故障</p></td>
<td align="left"><p>注册失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>22-拥塞</p></td>
<td align="left"><p>注册失败，因为网络拥塞。</p></td>
</tr>
</tbody>
</table>

 

例如，如果网络启动停用上下文事件，原因是不允许在位置区域中进行漫游，微型端口驱动程序应按照基于 GSM 的网络的 3GPP TS 24.008 原因代码，将**uNwError**成员设置为13。

类似的逻辑也应该应用于基于 CDMA 的网络。 但是，基于 CDMA 的网络错误代码没有标准。 基于 CDMA 的设备应使用特定于网络或特定于设备的错误代码。

在微型端口驱动程序对 OID 请求的异步响应的情况下，NDIS\_状态\_指示结构的**RequestId**成员是一个非零数字，作为*集*或*查询*请求的一部分传递到微型端口驱动程序。 微型端口驱动程序必须根据需要填充**uStatus**成员。 例如，WWAN\_状态\_SUCCESS，或者下一节中列出的任何适当的错误值。 除此之外，微型端口驱动程序必须在适当的和可用的位置填写**uNwError**成员。

### <a name="event-notification-status"></a>事件通知状态

下表列出了在 NDIS\_WWAN\_XXX 事件通知结构的**uStatus**成员中，MB 微型端口驱动程序可以指定的 WWAN\_状态代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_SUCCESS</p></td>
<td align="left"><p>操作成功。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_FAILURE</p></td>
<td align="left"><p>操作失败（一般错误）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_BUSY</p></td>
<td align="left"><p>操作失败，因为设备正忙。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SIM_NOT_INSERTED</p></td>
<td align="left"><p>操作失败，因为 SIM 卡未完全插入设备。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_BAD_SIM</p></td>
<td align="left"><p>操作失败，因为 SIM 卡错误，无法再使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_PIN_REQUIRED</p></td>
<td align="left"><p>操作失败，因为必须输入 PIN 才能继续。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_PIN_DISABLED</p></td>
<td align="left"><p>由于 PIN 已禁用，操作失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_NOT_REGISTERED</p></td>
<td align="left"><p>操作失败，因为设备未注册到任何网络。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_PROVIDERS_NOT_FOUND</p></td>
<td align="left"><p>由于找不到网络提供程序，因此操作失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_NO_DEVICE_SUPPORT</p></td>
<td align="left"><p>操作失败，因为设备不支持此操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_PROVIDER_NOT_VISIBLE</p></td>
<td align="left"><p>操作失败，因为服务提供程序当前不可见。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_DATA_CLASS_NOT_AVAILABLE</p></td>
<td align="left"><p>操作失败，因为所请求的数据类不可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_PACKET_SVC_DETACHED</p></td>
<td align="left"><p>由于已分离数据包服务，操作失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_MAX_ACTIVATED_CONTEXTS</p></td>
<td align="left"><p>操作失败，因为已达到激活上下文的最大数目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_NOT_INITIALIZED</p></td>
<td align="left"><p>操作失败，因为设备正在初始化。 请在设备就绪状态更改为<strong>WwanReadyStateInitialized</strong>后重试该操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_VOICE_CALL_IN_PROGRESS</p></td>
<td align="left"><p>操作失败，因为正在进行语音呼叫。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_CONTEXT_NOT_ACTIVATED</p></td>
<td align="left"><p>操作失败，因为未激活上下文。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SERVICE_NOT_ACTIVATED</p></td>
<td align="left"><p>操作失败，因为服务未激活。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_INVALID_ACCESS_STRING</p></td>
<td align="left"><p>操作失败，因为访问字符串无效。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_INVALID_USER_NAME_PWD</p></td>
<td align="left"><p>操作失败，因为提供的用户名和/或密码无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_RADIO_POWER_OFF</p></td>
<td align="left"><p>操作失败，因为无线电当前已关机。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_INVALID_PARAMETERS</p></td>
<td align="left"><p>由于参数无效，操作失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_READ_FAILURE</p></td>
<td align="left"><p>由于读取失败，操作失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_WRITE_FAILURE</p></td>
<td align="left"><p>由于写入失败，操作失败。</p></td>
</tr>
</tbody>
</table>

 

下表显示了 SMS 特定状态值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_SMS_OPERATION_NOT_ALLOWED</p></td>
<td align="left"><p>由于不允许执行此操作，SMS 操作失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SMS_MEMORY_FAILURE</p></td>
<td align="left"><p>由于内存故障，SMS 操作失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_SMS_INVALID_MEMORY_INDEX</p></td>
<td align="left"><p>由于<em>OID_WWAN_SMS_READ 的内存</em>索引无效，SMS 操作失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SMS_UNKNOWN_SMSC_ADDRESS</p></td>
<td align="left"><p>SMS 操作失败，因为服务中心编号无效或未知。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_SMS_NETWORK_TIMEOUT</p></td>
<td align="left"><p>由于网络超时，SMS 操作失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SMS_MEMORY_FULL</p></td>
<td align="left"><p>SMS 操作失败，因为 SMS 消息存储已满。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_SMS_UNKNOWN_ERROR</p></td>
<td align="left"><p>由于未知错误（一般错误），SMS 操作失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SMS_FILTER_NOT_SUPPORTED</p></td>
<td align="left"><p>SMS 操作失败，因为不支持请求的筛选器类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_SMS_MORE_DATA</p></td>
<td align="left"><p>此事务尚未完成。 某些数据已返回，并且有更多数据需要返回。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SMS_LANG_NOT_SUPPORTED</p></td>
<td align="left"><p>由于不支持 SMS 语言，SMS 操作失败。 这仅适用于基于 CDMA 的设备。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_SMS_ENCODING_NOT_SUPPORTED</p></td>
<td align="left"><p>SMS 操作失败，因为不支持 SMS 编码。 这仅适用于基于 CDMA 的设备。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SMS_FORMAT_NOT_SUPPORTED</p></td>
<td align="left"><p>由于不支持短信格式，SMS 操作失败。</p></td>
</tr>
</tbody>
</table>

 

**请注意**  这些 wwan 特定的状态代码仅用于 NDIS\_WWAN\_XXX 结构的**uStatus**成员中的异步事务。

 

小型端口驱动程序使用事件通知来通知 MB 服务在其 MB 设备中发生对象状态更改，而不首先收到 OID 请求。 MB 服务使用事件通知仅更新其状态机。

请注意，在 NDIS 序列化发送到微型端口驱动程序的所有请求时，微型端口驱动程序可能不会按相同顺序返回响应。 这是因为微型端口驱动程序中的排队请求可能会并行处理。 因此，MB 服务确保两个请求相互依赖时，它不会发送第二个请求，直到微型端口驱动程序完成第一个请求。

### <a name="state-change-notification"></a>状态更改通知

通常情况下，微型端口驱动程序应始终通过事务通知或未经请求的事件通知通知 MB 服务有关其 MB 设备更新状态的信息。 下面是一些例外情况，其中不应存在微型端口驱动程序对已更新状态信息的响应。 MB 服务可以从其他操作的完成状态中确定更新的状态：

1.  当 PIN 状态发生更改时，微型端口驱动程序无需将 NDIS\_状态发送\_WWAN\_PIN\_列表事件指示，因为 MB 服务请求启用或禁用 PIN。

2.  微型端口驱动程序不需要在\_WWAN\_预配\_上下文*集*操作的情况中，将事务响应中预配上下文的已更新列表返回到 OID。

3.  微型端口驱动程序无需在对 OID\_WWAN\_首选\_提供程序*集*操作的已更新列表中进行响应。 MB 服务可以根据初始列表和*设置*操作的成功状态来确定此信息。

4.  微型端口驱动程序无需用当前 WWAN\_SMS\_配置值与 OID\_WWAN\_SMS\_配置*集*操作进行响应。

 

 





