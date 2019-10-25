---
title: OID_GEN_NETWORK_LAYER_ADDRESSES
description: 作为集，OID_GEN_NETWORK_LAYER_ADDRESSES OID 通知底层微型端口驱动程序和其他分层驱动程序与绑定实例相关联的网络层地址的列表。
ms.assetid: 4a75c2ca-1a58-462e-876a-a65cfe63441e
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_NETWORK_LAYER_ADDRESSES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2d49a908fc5f128d8c70f8adf30a66f159630a77
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824391"
---
# <a name="oid_gen_network_layer_addresses"></a>OID\_代\_网络\_层\_地址


作为一个集，OID\_代\_网络\_层\_地址 OID 通知底层微型端口驱动程序和其他分层驱动程序有关与绑定实例关联的网络层地址的列表。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
可选。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
可选。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
可选。

<a name="remarks"></a>备注
-------

绑定实例是调用传输与通过调用[**NdisOpenAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex)设置的驱动程序之间的绑定。 传输使用传输\_地址和 TA\_地址结构，通知底层微型端口驱动程序和其他分层驱动程序有关网络层地址的列表。 微型端口驱动程序和其他分层驱动程序使用兼容的网络\_地址\_列表和网络\_地址结构，定义如下，以设置绑定接口上网络层地址的列表。

```C++
typedef struct _NETWORK_ADDRESS_LIST {
  LONG  AddressCount; 
  USHORT  AddressType; 
  NETWORK_ADDRESS  Address[1]; 
} NETWORK_ADDRESS_LIST, *PNETWORK_ADDRESS_LIST;
```

此结构的成员包含以下信息：

<a href="" id="addresscount"></a>**AddressCount**  
指定**地址**成员的数组中列出的网络层地址的数目。

<a href="" id="addresstype"></a>**AddressType**  
指定发送此 OID 的协议类型。 仅当**AddressCount**成员设置为零时，此成员才有效。 **AddressCount**成员设置为零，通知微型端口驱动程序或其他分层驱动程序清除绑定接口上网络层地址的列表。 协议可以是以下值之一：

<a href="" id="ndis-protocol-id-default"></a>默认情况下，NDIS\_协议\_ID\_  
默认协议

<a href="" id="ndis-protocol-id-tcp-ip"></a>NDIS\_协议\_ID\_TCP\_IP  
TCP/IP 协议

<a href="" id="ndis-protocol-id-ipx"></a>\_IPX 的 NDIS\_协议\_ID  
NetWare IPX 协议

<a href="" id="ndis-protocol-id-nbf"></a>NDIS\_协议\_ID\_NBF  
NetBIOS 协议

<a href="" id="address"></a>**地址**  
网络\_地址类型的网络层地址的数组。 **AddressCount**成员指定此数组中的元素数。

```C++
typedef struct _NETWORK_ADDRESS {
  USHORT  AddressLength; 
  USHORT  AddressType; 
  UCHAR   Address[1]; 
} NETWORK_ADDRESS, *PNETWORK_ADDRESS;
```

此结构的成员包含以下信息：

<a href="" id="addresslength"></a>**AddressLength**  
指定此网络层地址的大小（以字节为单位）。 **Address**成员包含指定此地址的字节数组。

<a href="" id="addresstype"></a>**AddressType**  
指定发送此 OID 和此网络层地址的协议类型。 仅当网络\_地址\_列表结构中的**AddressCount**成员设置为非零值时，此成员才有效。 网络\_地址\_列表中的**AddressCount**成员设置为一个非零值，通知微型端口驱动程序或其他分层驱动程序更改绑定接口上网络层地址的列表。 协议类型在前面的列表中定义。

<a href="" id="address"></a>**地址**  
指定此网络层地址的字节数组。 **AddressLength**成员指定此数组中的字节数。

传输可以调用[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)函数，并可以传递[**NDIS\_oid\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构，该结构使用 OID\_生成\_网络\_层\_地址代码。 此调用通知绑定实例与该实例相关联的地址中的更改。 在此调用中，传输还在*NdisBindingHandle*参数中传递绑定的实例。 绑定实例是在传输和基础微型端口驱动程序或其他分层驱动程序之间设置的绑定。 对于此调用，传输应使用指向传输\_地址结构的指针填充 NDIS\_OID\_请求的**InformationBuffer**成员。 传输\_地址对应于网络\_地址\_列表结构并应包含网络层地址的列表。

假设传输通过一个中间驱动程序将地址传递到基础微型端口驱动程序。 如果中间驱动程序还需要地址，则应在将其传递到基础微型端口驱动程序之前记下它们。 基础微型端口驱动程序（特别是旧驱动程序）可以返回 "\_不\_支持的 NDIS\_状态" 或 "NDIS\_状态\_成功" 状态值。 基础微型端口驱动程序将操作的状态传播到传输。 如果中间驱动程序必须继续接收地址通知，并且如有必要，中间驱动程序应将状态更改为 NDIS\_状态\_成功。否则，传输可能会将 NDIS\_状态解释\_不\_支持，因为这表明基础微型端口驱动程序不需要传输问题的其他地址更新。 如果返回 NDIS\_状态\_SUCCESS，则传输有义务继续向基础驱动程序通知关联地址中的任何更改，包括添加和删除地址。

协议可将传输\_地址的**AddressCount**成员设置为零，通知微型端口驱动程序或其他分层驱动程序清除绑定接口上网络层地址的列表。 如果**AddressCount**设置为零，则 NETWORK\_ADDRESS\_列表中的**AddressType**成员有效并且网络\_地址结构中的**AddressType**成员无效。 另一方面，协议可以将**AddressCount**设置为一个非零值，通知微型端口驱动程序或其他分层驱动程序更改绑定接口上网络层地址的列表。 在这种情况下，网络\_地址\_列表中的**AddressType**成员无效，并且网络\_地址结构中的**AddressType**成员有效。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)

[**NdisOpenAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex)

 

 




