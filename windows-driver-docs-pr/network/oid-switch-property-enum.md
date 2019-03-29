---
title: OID_SWITCH_PROPERTY_ENUM
description: HYPER-V 可扩展交换机扩展问题的对象标识符 (OID) 方法请求的 OID_SWITCH_PROPERTY_ENUM 以获取数组。
ms.assetid: 45277355-4486-4CE0-ACBF-68D6BC6B79E7
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PROPERTY_ENUM 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6fbaa6e59eb4629788d1618762573ab6392a1bcb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564576"
---
# <a name="oidswitchpropertyenum"></a>OID\_交换机\_属性\_枚举


HYPER-V 可扩展交换机扩展发出对象标识符 (OID) 方法请求的 OID\_切换\_属性\_枚举以获取数组。 此数组包含与指定的条件匹配的预配的交换机策略。 数组中的每个元素指定可扩展交换机策略的属性。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向缓冲区的指针。 此缓冲区包含以下数据：

-   [ **NDIS\_切换\_属性\_枚举\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598253)结构，它指定为可扩展交换机策略参数枚举。

-   一个数组[ **NDIS\_交换机\_属性\_枚举\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh598250)结构。 每个这些结构包含有关可扩展交换机策略的信息。

    **请注意**  如果未指定可扩展交换机策略的实例，并用设置扩展，扩展设置**NumProperties**的成员[ **NDIS\_交换机\_属性\_ENUM\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598253)结构为零，并无[ **NDIS\_交换机\_属性\_ENUM\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh598250)返回结构。

     

<a name="remarks"></a>备注
-------

OID\_切换\_属性\_的 HYPER-V 可扩展交换机完成激活后，才必须发出枚举 OID。 请参阅[查询的 HYPER-V 可扩展交换机配置](https://msdn.microsoft.com/library/windows/hardware/hh598293)的更多详细信息。

与 OID 不同查询的请求[OID\_交换机\_端口\_属性\_枚举](oid-switch-port-property-enum.md)，该扩展不需要调用任何*ReferenceSwitchXxx*或*DereferenceSwitchXxx*函数时它会发出 OID\_切换\_属性\_枚举请求下可扩展交换机驱动程序堆栈。

**请注意**  如果在扩展插件接收 OID 方法请求的 OID\_交换机\_属性\_枚举，它必须完成的 OID 请求。 相反，它必须调用[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)可扩展交换机在驱动程序堆栈的下层 OID 请求转发。

 

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础的微型端口边缘完成 OID 查询请求的 OID\_切换\_属性\_枚举，并返回以下状态代码之一。

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
<td><p>信息缓冲区长度太小，无法返回<a href="https://msdn.microsoft.com/library/windows/hardware/hh598253" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PROPERTY_ENUM_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh598253)"> <strong>NDIS_SWITCH_PROPERTY_ENUM_PARAMETERS</strong> </a>结构和其数组<a href="https://msdn.microsoft.com/library/windows/hardware/hh598250" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PROPERTY_ENUM_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh598250)"> <strong>NDIS_SWITCH_PROPERTY_ENUM_INFO</strong> </a>元素。 可扩展交换机设置的基础的微型端口边缘<strong>数据。METHOD_INFORMATION。BytesNeeded</strong>中的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
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
<td><p>版本</p></td>
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

[**NDIS\_交换机\_属性\_枚举\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh598250)

[**NDIS\_交换机\_属性\_枚举\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598253)

[查询的 HYPER-V 可扩展交换机配置](https://msdn.microsoft.com/library/windows/hardware/hh598293)

 

 




