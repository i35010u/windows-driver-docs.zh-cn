---
title: OID_SWITCH_PARAMETERS
description: HYPER-V 可扩展交换机扩展发出一个对象标识符 (OID) 查询请求的 OID_SWITCH_PARAMETERS 获取可扩展交换机的配置数据。
ms.assetid: F2CA0BE5-ED21-4ACF-B26A-4F512D4B15C7
ms.date: 08/08/2017
keywords: -OID_SWITCH_PARAMETERS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f18f4fd53d3d9fbe16ef9b289499acc31d859ff9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386878"
---
# <a name="oidswitchparameters"></a>OID\_交换机\_参数


HYPER-V 可扩展交换机扩展发出对象标识符 (OID) 查询请求的 OID\_切换\_参数来获取可扩展交换机的配置数据。

如果 OID 查询请求成功，完成**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_交换机\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598220)结构。

<a name="remarks"></a>备注
-------

当扩展插件处理返回[ **NDIS\_交换机\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598220)结构，它必须假定的各种字符串的成员**NDIS\_交换机\_参数**结构，如**SwitchName**，是以 null 结尾。 这些字符串成员的数据类型是由类型定义[ **IF\_盘点\_字符串**](https://msdn.microsoft.com/library/windows/hardware/hh451419)结构。 扩展必须确定字符串长度的值从**长度**此结构的成员。

**请注意**  如果字符串以 null 结尾**长度**成员必须包括终止 null 字符。

 

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础的微型端口边缘完成 OID 查询请求的 OID\_切换\_参数，并返回一个的以下状态代码。

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
<td><p>信息缓冲区长度太小，无法返回 OID 查询请求的 OID_SWITCH_PARAMETERS 结构。 可扩展交换机设置的基础的微型端口边缘<strong>数据。QUERY_INFORMATION。BytesNeeded</strong>中的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
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

[**NDIS\_SWITCH\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh598220)

[**NdisFOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561830)

 

 




