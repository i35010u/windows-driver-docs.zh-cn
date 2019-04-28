---
title: MB 操作语义
description: MB 操作语义
ms.assetid: 5f04b7fd-3df3-4efa-bb26-c7f4cd3c9ebd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13bbaaa26143c7f05d21caaa0807995f34aa53b3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343281"
---
# <a name="mb-operational-semantics"></a>MB 操作语义


### <a name="asynchronous-transactions"></a>异步事务

MB 驱动程序模型使用 NDIS 中提供的异步通知机制假设 MB 服务和微型端口驱动程序之间的非阻塞操作语义 6.x。 此机制允许 MB 服务继续将 OID 请求发送到的微型端口驱动程序处理而无需等待当前操作完成。

异步事务是三次握手开头的初始请求，请求状态响应后, 跟，然后由事务的最终指示完成的。 它仅确认微型端口驱动程序已收到请求，请求状态响应是临时窗口。 后续的异步指示是事务性的它表示事务的完成。 微型端口驱动程序返回状态代码，以及生成的数据中的事务的指示。

### <a name="asynchronous-set-and-query-requests"></a>异步*设置*并*查询*请求

许多*设置*并*查询*MB 服务所使用的 OID 请求异步处理。 有关详细信息*设置*并*查询*OID 请求，请参阅[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)。 中的"WWAN 特定 Oid"表[MB 数据模型](mb-data-model.md)主题标识的 Oid 以异步方式处理。

下图表示的异步交互序列*查询*MB 服务和微型端口驱动程序之间的事务。 粗体表示 OID 标识符或事务流控制中的标签和中常规文本的标签表示 OID 结构中的重要标志。

![说明在移动宽带服务和微型端口驱动程序之间的异步查询事务的交互序列关系图](images/wwanasyncquerytransaction.png)

是两个相同的三次握手*查询*并*设置*请求。

除[OID\_WWAN\_驱动程序\_CAPS](https://msdn.microsoft.com/library/windows/hardware/ff569825)，所有其他特定于 MB 的 OID 请求微型端口驱动程序和 MB 之间按照信息交换的异步事务机制具有以下附加说明的服务：

-   微型端口驱动程序应该会按照在任何错误条件，如无效的 OID 请求的 OID 请求立即失败。

-   微型端口驱动程序必须返回正确的错误代码与任何特定于 WWAN 的错误条件 (例如，WWAN\_状态\_XXX) 中指定**uStatus**事件通知结构的成员。 微型端口驱动程序应也相应地填充中的成员，请按照**uStatus**成员，根据需要。 例如，填充微型端口驱动程序应**ContextState.uNwError**的成员[ **NDIS\_WWAN\_上下文\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567906)结构，如果可用。 但是，发生故障时处理 Oid 与 Pin 时，微型端口驱动程序可能不一定要在中指定的当前 PIN 状态信息**PinInfo.PinState**的成员[ **NDIS\_WWAN\_PIN\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567911)。

-   微型端口驱动程序应返回 NDIS\_状态\_指示\_作为临时的全都是异步的 OID 请求响应所需。

-   微型端口驱动程序应能够区分从其他原因导致的 OID 请求的设备状态更改。 微型端口驱动程序应该发送事务性所得 OID 请求的状态更改通知和他们应发送未经请求的事件通知的状态更改从其他原因。

-   微型端口驱动程序负责管理内核模式的内存，尽管 MB 服务最初分配的内存的请求。 MB 服务收到响应后从微型端口驱动程序后，该服务可能会发布 OID 请求分配给用户模式内存。

下图表示的异步交互序列*设置*MB 服务和微型端口驱动程序之间的事务。 粗体表示 OID 标识符或事务流控制中的标签和中常规文本的标签表示 OID 结构中的重要标志。

![说明设置异步事务移动宽带服务和微型端口驱动程序之间的交互序列关系图](images/wwanasyncsettransaction.png)

### <a name="asynchronous-response"></a>异步响应

*NDIS 6.0 规范*（随 Windows Vista 一起发布） 引入了一个新的状态代码和 NDIS\_状态\_指示\_必需，传达的异步性质的微型端口驱动程序微型端口驱动程序的临时响应 OID 请求中的 MB 服务的事务。

如中所述[MB 接口概述](mb-interface-overview.md)，MB 服务没有直接访问权限分配的 MB 微型端口驱动程序的内核模式内存。 假定要复制和由提供给 MB 服务一些中介，例如，WMI 在内核模式内存中存储的执行结果或[NDIS 筛选器驱动程序](ndis-filter-drivers2.md)。 因此，微型端口驱动程序可以释放已分配的内核模式内存后[ **NdisMIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563600)函数调用返回事务的指示。

在下面的过程介绍了微型端口驱动程序和 MB 服务必须遵循的握手过程。

### <a name="mb-miniport-driver-procedure"></a>MB 微型端口驱动程序的过程

收到 OID 的请求，微型端口驱动程序应执行以下步骤：

1.  在内核模式，将复制的内容中分配内存[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)与 OID 请求相关联的数据结构。

2.  请求的参数，请确保**RequestId**并**RequestHandle** OID 请求结构的成员也会被复制。 这些成员将使用更高版本中事务性*指示*。

3.  返回临时 NDIS\_状态\_指示\_必需状态响应，以通知 MB 服务微型端口驱动程序将以异步方式完成请求。

4.  在完成该操作，将结果存储在本地或驱动程序分配内存中，根据需要。

5.  调用[ **NdisMIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563600)函数，以通知 MB 服务是否已完成未完成的操作。 微型端口驱动程序的 NDIS 成员中应填充\_状态\_指示结构，如下所示：
    1.  设置**StatusCode**状态通知的类型的成员。 例如，NDIS\_状态\_WWAN\_XXX。
    2.  设置**DestinationHandle**成员添加到**RequestHandle** NDIS 中收到的成员\_OID\_请求数据结构的微型端口驱动程序收到相应的 OID 请求。
    3.  设置**RequestId**成员以匹配**RequestId** NDIS 成员\_OID\_请求状态结构微型端口驱动程序收到相应的 OID 请求时。
    4.  设置**StatusBuffer**并**StatusBufferSize**成员分别指向微型端口驱动程序分配内存和内存缓冲区的大小。 此内存缓冲区包含已完成的操作的结果。
    5.  如果操作成功完成，设置**uStatus**成员添加到 WWAN\_状态\_成功。 否则，设置**uStatus**成员添加到相应 WWAN\_状态\_XXX 值，以指示失败的类型。

6.  函数调用返回时，微型端口驱动程序应释放它分配给 OID 请求的内存。

### <a name="mb-service-procedure"></a>MB 服务过程

MB 服务通过使用以下过程来处理异步事务：

1.  为基于 OID 数据结构的请求分配缓冲区内存。 填充数据使用适当的值的结构成员。

2.  调用[ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710)函数与**InformationBuffer**成员指向 OID 数据结构 OID 请求并等待到微型端口驱动程序响应。

3.  收到的 NDIS\_状态\_指示\_必需从微型端口驱动程序，MB 服务保存的临时响应**RequestId**，释放分配的内存，并将标记为打开的事务。 此时，MB 服务可以自由地处理后续 OID 请求并通知。

4.  收到一个通知，其中 NDIS\_状态\_WWAN\_为 XXX **StatusCode**值，检查是否**RequestId**匹配的任何事务标记为未结。 如果没有匹配项，该服务将关闭该事务。 如果不找到任何匹配项，则将视为未经请求的事件通知的通知。

5.  处理中返回的数据**StatusBuffer**成员并使状态更改为根据 MB 服务。

### <a name="indications"></a>指示

有两种类型的特定 WWAN*迹象*微型端口驱动程序可以生成：

-   产生的 MB 设备中的对象状态更改的事件通知。

-   指示异步操作已完成的事务通知。

在这两种情况下，微型端口驱动程序应调用 NdisMIndicateStatusEx 函数。

### <a name="event-notification"></a>事件通知

事件通知是未经请求的微型端口驱动程序主动向 MB 服务的状态更改事件发送所指示的局限性。 状态更改是由从 MB 服务以外的某个实体的操作导致的。 MB 服务会假定微型端口驱动程序都能够检测更改的原因。

对于任何 WWAN 特定的事件通知，必须设置微型端口驱动程序**RequestId**成员的 NDIS\_状态\_指示结构为零。 **StatusCode**成员指定的 MB 设备中的哪个对象已更改。 微型端口驱动程序可以将此对象设置为以下值之一：

[**NDIS\_STATUS\_WWAN\_DEVICE\_CAPS**](https://msdn.microsoft.com/library/windows/hardware/ff567845)

[**NDIS\_状态\_WWAN\_准备\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567856)

[**NDIS\_STATUS\_WWAN\_RADIO\_STATE**](https://msdn.microsoft.com/library/windows/hardware/ff567855)

[**NDIS\_状态\_WWAN\_PIN\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567851)

[**NDIS\_STATUS\_WWAN\_PIN\_LIST**](https://msdn.microsoft.com/library/windows/hardware/ff567852)

[**NDIS\_状态\_WWAN\_主页\_提供程序**](https://msdn.microsoft.com/library/windows/hardware/ff567848)

[**NDIS\_STATUS\_WWAN\_PREFERRED\_PROVIDERS**](https://msdn.microsoft.com/library/windows/hardware/ff567853)

[**NDIS\_状态\_WWAN\_VISIBLE\_提供程序**](https://msdn.microsoft.com/library/windows/hardware/ff567866)

[**NDIS\_状态\_WWAN\_注册\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567857)

[**NDIS\_STATUS\_WWAN\_PACKET\_SERVICE**](https://msdn.microsoft.com/library/windows/hardware/ff567850)

[**NDIS\_状态\_WWAN\_信号\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567859)

[**NDIS\_状态\_WWAN\_上下文\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567843)

[**NDIS\_状态\_WWAN\_已设置\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff567854)

[**NDIS\_状态\_WWAN\_服务\_激活**](https://msdn.microsoft.com/library/windows/hardware/ff567858)

[**NDIS\_状态\_WWAN\_SMS\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff567860)

[**NDIS\_STATUS\_WWAN\_SMS\_RECEIVE**](https://msdn.microsoft.com/library/windows/hardware/ff567862)

[**NDIS\_STATUS\_WWAN\_SMS\_SEND**](https://msdn.microsoft.com/library/windows/hardware/ff567863)

[**NDIS\_状态\_WWAN\_SMS\_删除**](https://msdn.microsoft.com/library/windows/hardware/ff567861)

[**NDIS\_STATUS\_WWAN\_SMS\_STATUS**](https://msdn.microsoft.com/library/windows/hardware/ff567864)

[**NDIS\_STATUS\_WWAN\_VENDOR\_SPECIFIC**](https://msdn.microsoft.com/library/windows/hardware/ff567865)

MB 服务还可以处理从 NDIS 其他事件通知。 这些非 MB 事件通知不一定是受要求的约束，其**RequestId**值将设置为零。

### <a name="transactional-notifications"></a>事务通知

微型端口驱动程序使用事务通知来通知异步事务已完成，MB 服务并 MB 服务使用事务通知，以关闭打开的事务并更新其状态的计算机。

MB 服务需要事务通知，以便它可以关闭打开的事务。 它是最终的三次握手 MB 服务和异步事务中的微型端口驱动程序之间交换。 值**RequestId**成员的 NDIS\_状态\_中任何事务通知指示必须为非零值，这从同一个事务中的相应请求复制。

必须设置**RequestId**成员的 NDIS\_状态\_指示结构正确的异步机制才能正常工作。 MB 服务可确保**RequestId**值是唯一的非零值中所有未完成的请求。 微型端口驱动程序必须返回相同**RequestId**中的相应值*指示*为了 MB 服务来关联与打开的事务的指示。

### <a name="status-indication-structure"></a>状态指示结构

这两个异步响应给定的 OID 请求和未经请求的事件通知结构共享以下指向的结构成员**StatusBuffer**的成员*StatusIndication*参数[ **NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600):

```C++
typedef struct _NDIS_WWAN_XXX {
  NDIS_OBJECT_HEADER Header;
  WWAN_STATUS uStatus;
  ULONG uNwError;//Optional. Only used for network operations.
  WWAN_XXX XxxStruct;
} NDIS_WWAN_XXX, *PNDIS_WWAN_XXX;
```

中的零值**RequestId**成员的 NDIS\_状态\_指示结构，这意味着它是未经请求的事件通知，可随时发生。

如果**uStatus**成员中返回的任何指示*设置*或*查询*OID 请求不等于 WWAN\_状态\_成功成员相关联的 NDIS\_WWAN\_XXX 结构不需要是有效的。

对于基于网络事件的未经请求的事件通知，微型端口驱动程序必须填写**uNwError**根据需要，如果适用的成员。

下表显示了注册，数据包将附加和分离中定义的原因代码失败值的数据包*3GPP TS 24.008 规范*基于 GSM 的网络：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">3GPP 24.008 原因代码</th>
<th align="left">解释的原因代码</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>2-国际移动 (IMSI) 未知中消隐</p></td>
<td align="left"><p>Sim 卡或设备未激活，或者订阅已过期，导致网络停用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4-IMSI VLR 中未知</p></td>
<td align="left"><p>未订阅漫游功能。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6-非法我</p></td>
<td align="left"><p>由于被盗的报表的网络被阻止的 MS。</p></td>
</tr>
<tr class="even">
<td align="left"><p>7-GPRS 服务不允许</p></td>
<td align="left"><p>用户不具有 GPRS 订阅。 用户必须仅语音连接订阅。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>8-GPRS 和非 GPRS 服务不允许</p></td>
<td align="left"><p>不允许使用 GPRS 和非 GPRS 服务。</p></td>
</tr>
<tr class="even">
<td align="left"><p>11-PLMN 不允许</p></td>
<td align="left"><p>由于过期的订阅或另一个原因网络阻止服务。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>12-位置区域不允许</p></td>
<td align="left"><p>用户订阅不允许存在的位置区域中的访问权限。</p></td>
</tr>
<tr class="even">
<td align="left"><p>13-漫游不允许在此位置区域</p></td>
<td align="left"><p>订阅允许漫游，但存在位置区域中不允许漫游。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>14-不允许在此 PLMN GPRS 服务</p></td>
<td align="left"><p>所选的网络提供商不提供对 MS GPRS 服务。</p></td>
</tr>
<tr class="even">
<td align="left"><p>15-没有合适的单元格位置区域中</p></td>
<td align="left"><p>没有为服务的的订阅。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>17-网络故障</p></td>
<td align="left"><p>注册失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>22-拥塞</p></td>
<td align="left"><p>由于网络拥塞，注册失败。</p></td>
</tr>
</tbody>
</table>

 

例如，如果网络启动停用上下文事件，因为位置区域中不允许漫游，微型端口驱动程序应设置**uNwError**到 13 根据 GSM 基于网络的 3GPP TS 24.008 原因代码的成员。

类似的逻辑应应用到也基于 CDMA 的网络。 但是，没有任何标准，用于基于 CDMA 的网络错误代码。 基于 CDMA 的设备应使用网络的特定或特定于设备的错误代码。

在 OID 请求微型端口驱动程序的异步响应的情况下**RequestId**成员的 NDIS\_状态\_指示结构是一个非零数字传递给过程的微型端口驱动程序*设置*或*查询*请求。 微型端口驱动程序必须填写**uStatus**作为相应的成员。 例如，WWAN\_状态\_下面的部分中列出的成功或任何相应的错误值。 除此之外，微型端口驱动程序必须填写**uNwError**成员相应和可用的位置。

### <a name="event-notification-status"></a>事件通知状态

下表列出了 WWAN\_MB 微型端口驱动程序可以在中指定的状态代码**uStatus** NDIS 成员\_WWAN\_XXX 事件通知结构。

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
<td align="left"><p>操作失败 （一般性失败）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_BUSY</p></td>
<td align="left"><p>操作失败，因为设备正忙。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SIM_NOT_INSERTED</p></td>
<td align="left"><p>操作失败，因为 SIM 卡未完全插入到设备。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_BAD_SIM</p></td>
<td align="left"><p>操作失败，因为 SIM 卡已损坏，无法进一步使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_PIN_REQUIRED</p></td>
<td align="left"><p>操作失败，因为必须输入 PIN 以继续。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_PIN_DISABLED</p></td>
<td align="left"><p>操作失败，因为 PIN 已被禁用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_NOT_REGISTERED</p></td>
<td align="left"><p>操作失败，因为设备未注册到任何网络。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_PROVIDERS_NOT_FOUND</p></td>
<td align="left"><p>操作失败，因为找不到任何网络提供程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_NO_DEVICE_SUPPORT</p></td>
<td align="left"><p>操作失败，因为设备不支持该操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_PROVIDER_NOT_VISIBLE</p></td>
<td align="left"><p>操作失败，因为服务提供程序当前不可见。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_DATA_CLASS_NOT_AVAILABLE</p></td>
<td align="left"><p>操作失败，因为请求的数据类不可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_PACKET_SVC_DETACHED</p></td>
<td align="left"><p>操作失败，因为数据包服务分离。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_MAX_ACTIVATED_CONTEXTS</p></td>
<td align="left"><p>操作失败，因为已达到激活上下文的最大数目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_NOT_INITIALIZED</p></td>
<td align="left"><p>操作失败，因为设备正在进行初始化。 重试该操作后设备就绪状态将变为<strong>WwanReadyStateInitialized</strong>。</p></td>
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
<td align="left"><p>该操作失败，因为用户名和/或提供的密码无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_RADIO_POWER_OFF</p></td>
<td align="left"><p>操作失败，因为单选当前处于关闭状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_INVALID_PARAMETERS</p></td>
<td align="left"><p>由于参数无效，操作失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_READ_FAILURE</p></td>
<td align="left"><p>该操作失败，因为读取失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_WRITE_FAILURE</p></td>
<td align="left"><p>该操作失败，因为写入错误。</p></td>
</tr>
</tbody>
</table>

 

下表显示了 SMS 特定状态的值。

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
<td align="left"><p>SMS 操作失败，因为不允许的操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SMS_MEMORY_FAILURE</p></td>
<td align="left"><p>SMS 操作失败，因为存在内存故障。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_SMS_INVALID_MEMORY_INDEX</p></td>
<td align="left"><p>SMS 操作失败，因为无效内存索引- <em>WwanSmsFlagIndex</em> OID_WWAN_SMS_READ 的。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SMS_UNKNOWN_SMSC_ADDRESS</p></td>
<td align="left"><p>SMS 操作失败，因为服务 center 数是无效或未知。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_SMS_NETWORK_TIMEOUT</p></td>
<td align="left"><p>SMS 操作由于网络超时而失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SMS_MEMORY_FULL</p></td>
<td align="left"><p>SMS 操作失败，因为 SMS 消息存储区已满。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_SMS_UNKNOWN_ERROR</p></td>
<td align="left"><p>SMS 操作失败，因为出现未知错误 （泛型错误）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SMS_FILTER_NOT_SUPPORTED</p></td>
<td align="left"><p>SMS 操作失败，因为不支持请求的筛选器类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_SMS_MORE_DATA</p></td>
<td align="left"><p>此事务尚未完成。 返回一些数据，并且没有要返回的更多数据。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SMS_LANG_NOT_SUPPORTED</p></td>
<td align="left"><p>SMS 操作失败，因为不支持的短信语言。 这仅适用于基于 CDMA 的设备。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_SMS_ENCODING_NOT_SUPPORTED</p></td>
<td align="left"><p>SMS 操作失败，因为 SMS 编码不受支持。 这仅适用于基于 CDMA 的设备。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SMS_FORMAT_NOT_SUPPORTED</p></td>
<td align="left"><p>SMS 操作失败，因为不支持 SMS 格式。</p></td>
</tr>
</tbody>
</table>

 

**请注意**  WWAN 特定状态代码仅用于在异步事务**uStatus** NDIS 成员\_WWAN\_XXX 结构。

 

微型端口驱动程序使用事件通知来告知而不必首先其 MB 设备中的对象状态更改 MB 服务收到的 OID 请求。 MB 服务使用事件通知来更新其状态机。

请注意，虽然 NDIS 序列化为发送到微型端口驱动程序的所有请求，微型端口驱动程序可能不返回响应中相同的顺序。 这是因为微型端口驱动程序中的排队的请求可能会并行处理。 因此 MB 服务可确保，如果两个请求都是相互依赖，它不会发送第二个请求微型端口驱动程序完成的第一个请求之前。

### <a name="state-change-notification"></a>状态更改通知

一般情况下，微型端口驱动程序应始终通知有关其事务通知或通过未经请求的事件通知的 MB 设备的更新状态 MB 服务。 以下方案是一些例外情况的微型端口驱动程序不应使用更新后的状态信息进行响应。 MB 服务可以确定其他操作的完成状态从更新后的状态：

1.  微型端口驱动程序不需要发送 NDIS\_状态\_WWAN\_PIN\_列表事件指示 MB 服务请求启用或禁用 PIN，因此发生 PIN 状态更改时。

2.  微型端口驱动程序不需要在 OID 的事务响应中返回的预配的上下文的更新的列表\_WWAN\_已预配\_上下文*设置*操作。

3.  微型端口驱动程序不需要使用更新中对 OID 的事务响应的首选提供程序的列表进行响应\_WWAN\_PREFERRED\_提供程序*设置*操作。 MB 服务可以确定此信息基于的初始列表和成功状态*设置*操作。

4.  微型端口驱动程序不需要使用当前 WWAN 进行响应\_短信\_OID 的配置值\_WWAN\_SMS\_配置*设置*操作。

 

 





