---
title: OID_RECEIVE_FILTER_ENUM_FILTERS
description: 基础驱动程序发出 OID_RECEIVE_FILTER_ENUM_FILTERS OID 方法的请求，以获取网络适配器配置的所有筛选器的列表。
ms.assetid: 498c1e96-c3ee-4f5d-b0f2-6e88921187e5
ms.date: 08/08/2017
keywords: -OID_RECEIVE_FILTER_ENUM_FILTERS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4eead4c8515dad96047aad47035da06f5304752b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349416"
---
# <a name="oidreceivefilterenumfilters"></a>OID\_RECEIVE\_FILTER\_ENUM\_FILTERS


基础驱动程序发出 OID 方法请求的 OID\_接收\_筛选器\_枚举\_筛选器，以获取网络适配器配置的所有筛选器的列表。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_接收\_筛选器\_信息\_数组**](https://msdn.microsoft.com/library/windows/hardware/ff567179)结构。

通过 OID 方法请求成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含指向缓冲区的指针。 此缓冲区已格式化为包含以下信息：

-   [ **NDIS\_接收\_筛选器\_信息\_数组**](https://msdn.microsoft.com/library/windows/hardware/ff567179)结构，它指定当前配置的接收筛选器的列表微型端口驱动程序。

-   一个数组[ **NDIS\_接收\_筛选器\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567176)结构。 每个结构指定的参数的微型端口驱动程序当前配置的接收筛选器。

<a name="remarks"></a>备注
-------

NDIS 接收筛选器在以下的 NDIS 接口中使用：

-   [NDIS 数据包合并](https://msdn.microsoft.com/library/windows/hardware/hh451601)。 详细了解如何使用此接口中接收的筛选器，请参阅[管理数据包合并接收筛选器](https://msdn.microsoft.com/library/windows/hardware/hh464026)。

-   [单根 I/O 虚拟化 (SR-IOV)](https://msdn.microsoft.com/library/windows/hardware/hh440235)。 详细了解如何使用此接口中接收的筛选器，请参阅[上虚拟端口设置接收的筛选器](https://msdn.microsoft.com/library/windows/hardware/hh440224)。

-   [虚拟机队列 (VMQ)](https://msdn.microsoft.com/library/windows/hardware/ff571035)。 详细了解如何使用此接口中接收的筛选器，请参阅[设置和清除 VMQ 筛选器](https://msdn.microsoft.com/library/windows/hardware/ff570780)。

基础驱动程序或应用程序颁发的 OID 的 OID 方法请求\_接收\_筛选器\_枚举\_筛选器，以枚举网络适配器设置的接收筛选器。 这包括接收的 SR-IOV 虚拟端口 (VPort) 设置的筛选器或 VMQ 接收队列。

### <a name="additional-guidelines-for-the-ndis-packet-coalescing-interface"></a>NDIS 数据包合并接口的其他准则

默认从 Windows Server 2012，合并仅支持 NDIS 数据包开始接收网络适配器的队列。

若要枚举数据包合并接收筛选器，基础驱动程序必须设置**QueueId**的成员[ **NDIS\_接收\_筛选器\_信息\_数组**](https://msdn.microsoft.com/library/windows/hardware/ff567179)结构到 NDIS\_默认\_接收\_队列\_id。

### <a name="additional-guidelines-for-the-sr-iov-interface"></a>SR-IOV 接口的其他准则

从 Windows Server 2012 中，SR-IOV 接口仅支持默认接收队列虚拟端口 (VPort)。

若要枚举 VPort 接收筛选器，但基础驱动程序必须设置**QueueId**的成员[ **NDIS\_接收\_筛选器\_信息\_数组**](https://msdn.microsoft.com/library/windows/hardware/ff567179)结构到 NDIS\_默认\_接收\_队列\_id。

### <a name="additional-guidelines-for-the-vmq-interface"></a>VMQ 接口的其他准则

基础驱动程序可以发出 OID 方法请求的 OID\_接收\_筛选器\_枚举\_筛选器，以枚举在 VMQ 设置的接收筛选器接收队列。 当基础驱动程序初始化[ **NDIS\_接收\_筛选器\_信息\_数组**](https://msdn.microsoft.com/library/windows/hardware/ff567179)结构，它会设置**QueueId**成员添加到以下值之一：

-   非默认的队列标识符值接收队列。 基础驱动程序从较早的 OID 方法请求获取队列标识符输入的值[OID\_接收\_筛选器\_分配\_队列](oid-receive-filter-allocate-queue.md)或 OID 查询请求的[OID\_接收\_筛选器\_枚举\_队列](oid-receive-filter-enum-queues.md)。

-   队列标识符值的 NDIS\_默认\_接收\_队列\_ID，它指定默认接收队列。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID 方法请求的 OID\_接收\_筛选器\_枚举\_微型端口驱动程序，并返回一个的以下状态代码的筛选器：

<a href="" id="ndis-status-success"></a>NDIS\_状态\_成功  
请求已成功完成。 **InformationBuffer**指向[ **NDIS\_接收\_筛选器\_信息\_数组**](https://msdn.microsoft.com/library/windows/hardware/ff567179)结构。

<a href="" id="ndis-status-pending"></a>NDIS\_状态\_PENDING  
请求正在等待完成。 请求完成后项目，NDIS 都会将最终状态代码和结果传递给调用方的 OID 请求完成处理程序中。

<a href="" id="ndis-status-invalid-length"></a>NDIS\_状态\_无效\_长度  
信息缓冲区太短。 NDIS 集**数据。查询\_信息。BytesNeeded**中的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)是必需的最小缓冲区大小的结构。

<a href="" id="ndis-status-failure"></a>NDIS\_状态\_失败  
请求由于其他原因而失败。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>支持 NDIS 6.20 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_RECEIVE\_FILTER\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff567176)

[**NDIS\_接收\_筛选器\_信息\_数组**](https://msdn.microsoft.com/library/windows/hardware/ff567179)

[OID\_RECEIVE\_FILTER\_ALLOCATE\_QUEUE](oid-receive-filter-allocate-queue.md)

[OID\_RECEIVE\_FILTER\_ENUM\_QUEUES](oid-receive-filter-enum-queues.md)

[OID\_RECEIVE\_FILTER\_SET\_FILTER](oid-receive-filter-set-filter.md)

 

 




