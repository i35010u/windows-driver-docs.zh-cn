---
title: OID_GEN_NETWORK_LAYER_ADDRESSES
description: 作为一组 OID_GEN_NETWORK_LAYER_ADDRESSES OID 通知基础微型端口驱动程序和其他分层驱动程序有关的绑定实例与相关联的网络层地址的列表。
ms.assetid: 4a75c2ca-1a58-462e-876a-a65cfe63441e
ms.date: 08/08/2017
keywords: -OID_GEN_NETWORK_LAYER_ADDRESSES 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ae9e9aafe53f18a79e7941cdbc39a17bc7332cd2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564103"
---
# <a name="oidgennetworklayeraddresses"></a>OID\_GEN\_网络\_层\_地址


作为一组 OID\_GEN\_网络\_层\_地址 OID 通知基础微型端口驱动程序和其他分层驱动程序有关的绑定实例与相关联的网络层地址的列表。

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

绑定的实例，则调用传输和通过调用设置的驱动程序之间的绑定[ **NdisOpenAdapterEx**](https://msdn.microsoft.com/library/windows/hardware/ff563715)。 传输通道使用传输\_地址和 TA\_地址结构以通知基础微型端口驱动程序和其他分层驱动程序有关的网络层地址列表。 微型端口驱动程序和其他分层驱动程序使用兼容的网络\_地址\_列表和网络\_定义，如下所示，若要绑定接口上设置的网络层地址列表的地址结构。

```C++
typedef struct _NETWORK_ADDRESS_LIST {
  LONG  AddressCount; 
  USHORT  AddressType; 
  NETWORK_ADDRESS  Address[1]; 
} NETWORK_ADDRESS_LIST, *PNETWORK_ADDRESS_LIST;
```

此结构的成员包含下列信息：

<a href="" id="addresscount"></a>**AddressCount**  
指定的数组中列出的网络层地址数**地址**成员。

<a href="" id="addresstype"></a>**AddressType**  
指定将发送此 OID 的协议类型。 此成员才有效如果**AddressCount**成员设置为零。 **AddressCount**成员设置为零，以通知微型端口驱动程序或其他分层的驱动程序，以清除绑定接口上的网络层地址的列表。 该协议可以是下列值之一：

<a href="" id="ndis-protocol-id-default"></a>NDIS\_协议\_ID\_默认  
默认协议

<a href="" id="ndis-protocol-id-tcp-ip"></a>NDIS\_协议\_ID\_TCP\_IP  
TCP/IP 协议

<a href="" id="ndis-protocol-id-ipx"></a>NDIS\_协议\_ID\_IPX  
NetWare IPX 协议

<a href="" id="ndis-protocol-id-nbf"></a>NDIS\_PROTOCOL\_ID\_NBF  
NetBIOS 协议

<a href="" id="address"></a>**地址**  
数组类型网络的网络层地址\_地址。 **AddressCount**成员此数组中指定的元素数。

```C++
typedef struct _NETWORK_ADDRESS {
  USHORT  AddressLength; 
  USHORT  AddressType; 
  UCHAR   Address[1]; 
} NETWORK_ADDRESS, *PNETWORK_ADDRESS;
```

此结构的成员包含下列信息：

<a href="" id="addresslength"></a>**AddressLength**  
指定大小，以字节为单位，此网络层地址。 **地址**成员包含指定此地址的字节数组。

<a href="" id="addresstype"></a>**AddressType**  
指定将发送此 OID 和此网络层地址的协议类型。 此成员才有效如果**AddressCount**网络中的成员\_地址\_列表结构设置为非零值。 **AddressCount**网络中的成员\_地址\_列表设置为非零值，以通知微型端口驱动程序或其他分层的驱动程序，若要更改绑定接口上的网络层地址列表。 协议类型定义中前面的列表。

<a href="" id="address"></a>**地址**  
指定此网络层地址的字节数组。 **AddressLength**成员此数组中指定的字节数。

可以调用传输[ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710)函数，并可以传递[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构填充的 OID\_GEN\_网络\_层\_地址代码。 此调用通知中与该实例相关联的地址的更改的绑定的实例。 在此调用中，传输还将传递中的绑定的实例*NdisBindingHandle*参数。 绑定设置传输和基础微型端口驱动程序或其他分层驱动程序之间的绑定的实例。 对于此调用，传输应填充**InformationBuffer**成员的 NDIS\_OID\_用一个指针指向传输请求\_地址结构。 传输\_地址对应于网络\_地址\_列表结构，并且应包含的网络层地址列表。

假设传输将传递到基础的微型端口驱动程序的中间驱动程序通过地址。 如果中间驱动程序也需要地址，需要记下这些值之前将它们传递到基础微型端口驱动程序。 基础微型端口驱动程序，尤其是旧驱动程序，可以返回在 status 值为 NDIS\_状态\_不\_SUPPORTED 或 NDIS\_状态\_成功。 基础的微型端口驱动程序将备份操作的状态传播针对传输中。 如果中间驱动程序必须继续接收地址通知，并且如有必要，中间驱动程序应将状态更改为 NDIS\_状态\_成功。否则，传输可能会解释 NDIS\_状态\_不\_支持，因为基础微型端口驱动程序不需要传输发出额外的地址的指示更新。 如果 NDIS\_状态\_成功返回、 传输有义务继续通知基础驱动程序的相关联的地址，包括添加和删除地址中的任何更改。

可以设置一种协议**AddressCount**传输成员\_为零的地址，以便微型端口驱动程序或其他分层的驱动程序，以清除绑定接口上的网络层地址的列表。 如果**AddressCount**设置为零，则**AddressType**网络中的成员\_地址\_列表是否有效并**AddressType**中的成员网络\_地址结构不是有效。 但是，可以设置一种协议**AddressCount**为非零值，以通知微型端口驱动程序或其他分层的驱动程序，若要更改绑定接口上的网络层地址列表。 在这种情况下， **AddressType**网络中的成员\_地址\_列表不是有效并**AddressType**网络成员\_地址结构是否有效。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NdisOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff563710)

[**NdisOpenAdapterEx**](https://msdn.microsoft.com/library/windows/hardware/ff563715)

 

 




