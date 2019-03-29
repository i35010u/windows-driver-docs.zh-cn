---
title: OID_RECEIVE_FILTER_HARDWARE_CAPABILITIES
description: 基础驱动程序发出 OID 查询请求的 OID_RECEIVE_FILTER_HARDWARE_CAPABILITIES 以获取网络适配器的接收筛选硬件功能。
ms.assetid: 2b80944e-5309-4cb0-a69a-331f8fd3f7a4
ms.date: 08/08/2017
keywords: -OID_RECEIVE_FILTER_HARDWARE_CAPABILITIES 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 78d64ecb4baf0db3fcb15af9de2d75002ec0a8c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566414"
---
# <a name="oidreceivefilterhardwarecapabilities"></a>OID\_接收\_筛选器\_硬件\_功能


基础驱动程序发出 OID 查询请求的 OID\_接收\_筛选器\_硬件\_功能，以获取筛选的硬件功能的网络适配器的接收。

从 OID 查询请求，成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[**NDIS\_接收\_筛选器\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)结构。

<a name="remarks"></a>备注
-------

NDIS 接收筛选器在以下的 NDIS 接口中使用：

-   [NDIS 数据包合并](https://msdn.microsoft.com/library/windows/hardware/hh451601)。 详细了解如何使用此接口中接收的筛选器，请参阅[管理数据包合并接收筛选器](https://msdn.microsoft.com/library/windows/hardware/hh464026)。

-   [单根 I/O 虚拟化 (SR-IOV)](https://msdn.microsoft.com/library/windows/hardware/hh440235)。 详细了解如何使用此接口中接收的筛选器，请参阅[上虚拟端口设置接收的筛选器](https://msdn.microsoft.com/library/windows/hardware/hh440224)。

-   [虚拟机队列 (VMQ)](https://msdn.microsoft.com/library/windows/hardware/ff571035)。 详细了解如何使用此接口中接收的筛选器，请参阅[设置和清除 VMQ 筛选器](https://msdn.microsoft.com/library/windows/hardware/ff570780)。

[ **NDIS\_接收\_筛选器\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)结构包含有关接收筛选的网络适配器的硬件功能信息. 这些功能可以包括硬件功能由 INF 文件设置或通过当前已禁用**高级**属性页。

**请注意**  接收筛选硬件的所有功能的网络适配器都返回通过 OID 查询请求的 OID\_接收\_筛选器\_硬件\_功能，而不考虑的一项功能是启用还是禁用。

 

从 NDIS 6.20 微型端口驱动程序当前已启用的注册接收筛选硬件功能的网络适配器时其[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)调用函数。 微型端口驱动程序通过执行以下步骤来注册这些功能：

1.  该驱动程序初始化[ **NDIS\_接收\_筛选器\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)与接收筛选硬件功能的结构。

2.  该驱动程序初始化[ **NDIS\_微型端口\_适配器\_硬件\_协助\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)结构和集**CurrentReceiveFilterCapabilities**指向的指针到成员[ **NDIS\_接收\_筛选器\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)结构。

3.  微型端口驱动程序调用[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)函数和集*MiniportAttributes*参数指向的[ **NDIS\_微型端口\_适配器\_硬件\_帮助\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)结构。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID 查询请求的 OID\_接收\_筛选器\_硬件\_的微型端口驱动程序，并返回一个以下状态代码的功能：

<a href="" id="ndis-status-success"></a>NDIS\_状态\_成功  
请求已成功完成。 **InformationBuffer**指向[ **NDIS\_接收\_筛选器\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)结构。

<a href="" id="ndis-status-pending"></a>NDIS\_状态\_PENDING  
请求正在等待完成。 请求完成后项目，NDIS 都会将最终状态代码和结果传递给调用方的 OID 请求完成处理程序中。

<a href="" id="ndis-status-invalid-length"></a>NDIS\_状态\_无效\_长度  
信息缓冲区太短。 NDIS 集**数据。查询\_信息。BytesNeeded**中的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)是必需的最小缓冲区大小的结构。

<a href="" id="ndis-status-not-supported"></a>NDIS\_状态\_不\_支持  
网络适配器不支持接收筛选。

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


[**NDIS\_BIND\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff564832)

[**NDIS\_微型端口\_适配器\_硬件\_帮助\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_RECEIVE\_FILTER\_CAPABILITIES**](https://msdn.microsoft.com/library/windows/hardware/ff566864)

 

 




