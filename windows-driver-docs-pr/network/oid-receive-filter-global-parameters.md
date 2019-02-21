---
title: OID_RECEIVE_FILTER_GLOBAL_PARAMETERS
description: 基础驱动程序发出请求来获取全局 OID_RECEIVE_FILTER_GLOBAL_PARAMETERS 接收的网络适配器的筛选参数 OID 查询。
ms.assetid: be6f7210-d1f9-4490-838a-806488df41da
ms.date: 08/08/2017
keywords: -OID_RECEIVE_FILTER_GLOBAL_PARAMETERS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6e84ea157bbe706ea834a065ef594604595bde00
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555944"
---
# <a name="oidreceivefilterglobalparameters"></a>OID\_接收\_筛选器\_GLOBAL\_参数


基础驱动程序发出 OID 查询请求的 OID\_接收\_筛选器\_GLOBAL\_参数来获取全局接收的网络适配器的筛选参数。

从 OID 查询请求，成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_接收\_筛选器\_全局\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567171)结构。

<a name="remarks"></a>备注
-------

NDIS 接收筛选器在以下的 NDIS 接口中使用：

-   [NDIS 数据包合并](https://msdn.microsoft.com/library/windows/hardware/hh451601)。 详细了解如何使用此接口中接收的筛选器，请参阅[管理数据包合并接收筛选器](https://msdn.microsoft.com/library/windows/hardware/hh464026)。

-   [单根 I/O 虚拟化 (SR-IOV)](https://msdn.microsoft.com/library/windows/hardware/hh440235)。 详细了解如何使用此接口中接收的筛选器，请参阅[上虚拟端口设置接收的筛选器](https://msdn.microsoft.com/library/windows/hardware/hh440224)。

-   [虚拟机队列 (VMQ)](https://msdn.microsoft.com/library/windows/hardware/ff571035)。 详细了解如何使用此接口中接收的筛选器，请参阅[设置和清除 VMQ 筛选器](https://msdn.microsoft.com/library/windows/hardware/ff570780)。

从开始 NDIS 6.20，协议驱动程序使用 OID\_接收\_筛选器\_GLOBAL\_参数进行查询的当前全局配置参数接收的网络适配器上筛选。 例如，协议驱动程序可以使用此 OID 以确定是否将筛选器类型的接收或接收队列启用或禁用。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID 查询请求的 OID\_接收\_筛选器\_GLOBAL\_微型端口驱动程序，并返回一个的以下状态代码的参数：

<a href="" id="ndis-status-success"></a>NDIS\_状态\_成功  
请求已成功完成。

<a href="" id="ndis-status-pending"></a>NDIS\_状态\_PENDING  
请求正在等待完成。 请求完成后项目，NDIS 都会将最终状态代码和结果传递给调用方的 OID 请求完成处理程序中。

<a href="" id="ndis-status-invalid-length"></a>NDIS\_状态\_无效\_长度  
信息缓冲区太短。 NDIS 集**数据。查询\_信息。BytesNeeded**中的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)是必需的最小缓冲区大小的结构。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_状态\_无效\_参数  
请求失败，因为它尝试启用的基础网络适配器不支持的功能。

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
<td><p>标头</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_接收\_筛选器\_GLOBAL\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567171)

 

 




