---
title: OID_SWITCH_NIC_ARRAY
description: HYPER-V 可扩展交换机扩展问题的对象标识符 (OID) 查询请求的 OID_SWITCH_NIC_ARRAY 以获取数组。
ms.assetid: CA9958DF-4389-4B4F-B110-03F500E27A1B
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_ARRAY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1e1e53c4320b7e77ae90f56e356aa0998428cc07
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351257"
---
# <a name="oidswitchnicarray"></a>OID\_SWITCH\_NIC\_ARRAY


HYPER-V 可扩展交换机扩展发出对象标识符 (OID) 查询请求的 OID\_切换\_NIC\_以获取数组的数组。 数组中的每个元素指定与可扩展交换机端口相关联的虚拟网络适配器的配置参数。

如果成功，完成 OID 查询请求**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含指向缓冲区的指针。 此缓冲区包含以下数据：

-   [ **NDIS\_交换机\_NIC\_数组**](https://msdn.microsoft.com/library/windows/hardware/hh598212)结构，它定义数组中的元素数。 此结构还指定数组中的第一个元素的偏移量。

-   一个数组[ **NDIS\_交换机\_NIC\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598215)结构。 每个这些结构包含有关连接到可扩展交换机端口的网络适配器的信息。

    **请注意**  没有网络适配器已连接到可扩展交换机端口，如果设置的可扩展交换机基础的微型端口边缘**NumElements**的成员[ **NDIS\_交换机\_NIC\_数组**](https://msdn.microsoft.com/library/windows/hardware/hh598212)为零的结构。 在这种情况下，没有[ **NDIS\_交换机\_NIC\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598215)返回结构。

     

<a name="remarks"></a>备注
-------

OID\_切换\_NIC\_的 HYPER-V 可扩展交换机完成激活后，才必须发出数组 OID。 请参阅[查询的 HYPER-V 可扩展交换机配置](https://msdn.microsoft.com/library/windows/hardware/hh598293)的更多详细信息。

当扩展插件处理返回[ **NDIS\_交换机\_NIC\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598215)结构，它必须假定的各种字符串的成员[**NDIS\_交换机\_端口\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598229)结构，如**NicFriendlyName**，是以 NULL 结尾。 这些字符串成员的数据类型是由类型定义[ **IF\_盘点\_字符串**](https://msdn.microsoft.com/library/windows/hardware/hh451419)结构。 该驱动程序必须确定字符串长度的值从**长度**此结构的成员。

**请注意**  如果字符串以 null 结尾**长度**成员必须包括终止 null 字符。

 

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础的微型端口边缘完成 OID 查询请求的 OID\_切换\_NIC\_数组并返回一个的以下状态代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态代码</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>OID 请求已成功完成。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区长度太小，无法返回<a href="https://msdn.microsoft.com/library/windows/hardware/hh598212" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_NIC_ARRAY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh598212)"> <strong>NDIS_SWITCH_NIC_ARRAY</strong> </a>和其数组<a href="https://msdn.microsoft.com/library/windows/hardware/hh598215" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_NIC_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh598215)"> <strong>NDIS_SWITCH_NIC_PARAMETERS</strong> </a>元素。 可扩展交换机设置的基础的微型端口边缘<strong>数据。QUERY_INFORMATION。BytesNeeded</strong>中的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>请求由于其他原因而失败。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_SWITCH\_NIC\_ARRAY**](https://msdn.microsoft.com/library/windows/hardware/hh598212)

[**NDIS\_SWITCH\_NIC\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh598215)

[查询的 HYPER-V 可扩展交换机配置](https://msdn.microsoft.com/library/windows/hardware/hh598293)

 

 




