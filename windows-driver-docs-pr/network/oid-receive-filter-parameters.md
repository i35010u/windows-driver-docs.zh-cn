---
title: OID_RECEIVE_FILTER_PARAMETERS
description: 基础驱动程序发出 OID_RECEIVE_FILTER_PARAMETERS OID 方法的请求，以获取网络适配器上的筛选器的当前配置参数。
ms.assetid: 1bb12945-0dad-47b9-9f44-e05efe292979
ms.date: 08/08/2017
keywords: -OID_RECEIVE_FILTER_PARAMETERS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 17503b1d9edc9b54073ddf6c2032b01e129b0bdb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567137"
---
# <a name="oidreceivefilterparameters"></a>OID\_RECEIVE\_FILTER\_PARAMETERS


基础驱动程序发出 OID 方法请求的 OID\_接收\_筛选器\_参数来获取网络适配器上的筛选器的当前配置参数。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_接收\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567181)结构。 使用 NDIS **FilterId**输入结构中的成员，若要标识筛选器。

通过 OID 方法请求成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含指向缓冲区的指针。 此缓冲区已格式化为包含以下信息：

-   [ **NDIS\_接收\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567181) ndis 指定的参数的结构接收筛选器。

-   一个数组[ **NDIS\_接收\_筛选器\_字段\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567169)结构指定的筛选器测试条件中的字段网络数据包标头。

<a name="remarks"></a>备注
-------

NDIS 接收筛选器在以下的 NDIS 接口中使用：

-   [NDIS 数据包合并](https://msdn.microsoft.com/library/windows/hardware/hh451601)。 详细了解如何使用此接口中接收的筛选器，请参阅[管理数据包合并接收筛选器](https://msdn.microsoft.com/library/windows/hardware/hh464026)。

-   [单根 I/O 虚拟化 (SR-IOV)](https://msdn.microsoft.com/library/windows/hardware/hh440235)。 详细了解如何使用此接口中接收的筛选器，请参阅[上虚拟端口设置接收的筛选器](https://msdn.microsoft.com/library/windows/hardware/hh440224)。

-   [虚拟机队列 (VMQ)](https://msdn.microsoft.com/library/windows/hardware/ff571035)。 详细了解如何使用此接口中接收的筛选器，请参阅[设置和清除 VMQ 筛选器](https://msdn.microsoft.com/library/windows/hardware/ff570780)。

基础驱动程序发出的 OID 的 OID 方法请求\_接收\_筛选器\_参数来获取网络适配器设置的接收筛选器的配置参数。 这包括设置 VMQ 接收队列或的 SR-IOV 虚拟端口 (VPort) 的接收筛选器以及已下载到微型端口驱动程序的数据包合并筛选器。

基础驱动程序从较早的 OID 方法请求获取筛选器标识符[OID\_接收\_筛选器\_设置\_筛选器](oid-receive-filter-set-filter.md)或 OID 请求从[OID\_接收\_筛选器\_ENUM\_筛选器](oid-receive-filter-enum-filters.md)。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID 请求的 OID\_接收\_筛选器\_微型端口驱动程序，并返回一个的以下状态代码的参数：

<a href="" id="ndis-status-success"></a>NDIS\_状态\_成功  
请求已成功完成。 **InformationBuffer**指向[ **NDIS\_接收\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567181)结构。

<a href="" id="ndis-status-pending"></a>NDIS\_状态\_PENDING  
请求正在等待完成。 请求完成后项目，NDIS 都会将最终状态代码和结果传递给调用方的 OID 请求完成处理程序中。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_状态\_无效\_参数  
基础驱动程序或应用程序提供的筛选器无效标识符。 如果为零，或者指定一个未定义的筛选器，筛选器标识符无效。

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
<td><p>版本</p></td>
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

[OID\_RECEIVE\_FILTER\_ENUM\_FILTERS](oid-receive-filter-enum-filters.md)

[**NDIS\_RECEIVE\_FILTER\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff567181)

[OID\_RECEIVE\_FILTER\_SET\_FILTER](oid-receive-filter-set-filter.md)

 

 




