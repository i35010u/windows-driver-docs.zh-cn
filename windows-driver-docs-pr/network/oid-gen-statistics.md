---
title: OID_GEN_STATISTICS
description: 作为查询，NDIS 和过量驱动程序使用 OID_GEN_STATISTICS OID 获取适配器或微型端口驱动程序的统计信息。
ms.assetid: ff81d6b0-806d-4ddf-9da1-a169221be61f
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_STATISTICS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a09f3c297bab6e09b6b3cc1d595aecd8ab99dbab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844600"
---
# <a name="oid_gen_statistics"></a>OID\_代\_统计信息


作为查询，NDIS 和过量驱动程序使用 OID\_GEN\_STATISTICS OID 获取适配器或微型端口驱动程序的统计信息。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
必需.

\_INFO 结构的 NDIS\_统计信息的定义如下：

```ManagedCPlusPlus
    typedef struct _NDIS_STATISTICS_INFO {
         NDIS_OBJECT_HEADER Header;
         ULONG SupportedStatistics;
         ULONG64 ifInDiscards;
         ULONG64 ifInErrors;
         ULONG64 ifHCInOctets;
         ULONG64 ifHCInUcastPkts;
         ULONG64 ifHCInMulticastPkts;
         ULONG64 ifHCInBroadcastPkts;
         ULONG64 ifHCOutOctets;
         ULONG64 ifHCOutUcastPkts;
         ULONG64 ifHCOutMulticastPkts;
         ULONG64 ifHCOutBroadcastPkts;
         ULONG64 ifOutErrors;
         ULONG64 ifOutDiscards;
         ULONG64 ifHCInUcastOctets;
         ULONG64 ifHCInMulticastOctets;
         ULONG64 ifHCInBroadcastOctets;
         ULONG64 ifHCOutUcastOctets;
         ULONG64 ifHCOutMulticastOctets;
         ULONG64 ifHCOutBroadcastOctets;
    } NDIS_STATISTICS_INFO, *PNDIS_STATISTICS_INFO;
```




此结构包含以下成员：

<a href="" id="header"></a>**标头**  
[**Ndis\_对象\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)用于 NDIS\_统计信息的标头结构\_信息结构。 将**标头**指定的结构的**类型**成员设置为\_对象\_类型\_默认值、ndis 的**修订**成员\_统计信息\_成员到 NDIS\_SIZEOF\_STATISTICS\_信息\_修订\_版本1。

<a href="" id="supportedstatistics"></a>**SupportedStatistics**  
微型端口驱动程序支持的统计信息集。

**注意** NDIS 6.0 和更高版本的驱动程序必须支持所有统计信息，并且在查询 OID\_代\_STATISTICS 时，必须对其进行报告。



该值是以下标志的按位 "或"：

<a href="" id="ndis-statistics-flags-valid-directed-frames-rcv"></a>NDIS\_统计信息\_标志\_有效\_定向\_帧\_RCV  
**IfHCInUcastPkts**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-multicast-frames-rcv"></a>NDIS\_统计信息\_标志\_有效\_多播\_帧\_RCV  
**IfHCInMulticastPkts**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-broadcast-frames-rcv"></a>NDIS\_统计信息\_标志\_有效\_广播\_帧\_RCV  
**IfHCInBroadcastPkts**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-bytes-rcv"></a>NDIS\_统计信息\_标志\_有效\_字节\_RCV  
**IfHCInOctets**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-rcv-discards"></a>NDIS\_统计信息\_标志\_有效\_RCV\_放弃  
**IfInDiscards**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-rcv-error"></a>NDIS\_统计信息\_标志\_有效\_RCV\_错误  
**IfInErrors**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-directed-frames-xmit"></a>NDIS\_统计信息\_标志\_有效\_定向\_帧\_XMIT  
**IfHCOutUcastPkts**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-multicast-frames-xmit"></a>NDIS\_统计信息\_标志\_有效\_多播\_帧\_XMIT  
**IfHCOutMulticastPkts**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-broadcast-frames-xmit"></a>NDIS\_统计信息\_标志\_有效\_广播\_帧\_XMIT  
**IfHCOutBroadcastPkts**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-bytes-xmit"></a>NDIS\_统计信息\_标志\_有效\_字节\_XMIT  
**IfHCOutOctets**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-xmit-error"></a>NDIS\_统计信息\_标志\_有效\_XMIT\_错误  
**IfOutErrors**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-xmit-discards"></a>NDIS\_统计信息\_标志\_有效\_XMIT\_放弃  
**IfOutDiscards**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-directed-bytes-rcv"></a>NDIS\_统计信息\_标志\_有效\_定向\_字节\_RCV  
**IfHCInUcastOctets**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-multicast-bytes-rcv"></a>NDIS\_统计信息\_标志\_有效\_多播\_字节\_RCV  
**IfHCInMulticastOctets**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-broadcast-bytes-rcv"></a>NDIS\_统计信息\_标志\_有效\_广播\_字节\_RCV  
**IfHCInBroadcastOctets**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-directed-bytes-xmit"></a>NDIS\_统计信息\_标志\_有效\_定向\_字节\_XMIT  
**IfHCOutUcastOctets**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-multicast-bytes-xmit"></a>NDIS\_统计信息\_标志\_有效\_多播\_字节\_XMIT  
**IfHCOutMulticastOctets**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-broadcast-bytes-xmit"></a>NDIS\_统计信息\_标志\_有效\_广播\_字节\_XMIT  
**IfHCOutBroadcastOctets**成员中的数据是有效的。

<a href="" id="ifindiscards"></a>**ifInDiscards**  
丢弃的接收缓冲区错误计数。 此值与[OID\_代\_RCV\_放弃](oid-gen-rcv-discards.md)返回的值相同。

<a href="" id="ifinerrors"></a>**ifInErrors**  
接收错误计数。 此计数与[OID\_代\_RCV\_错误](oid-gen-rcv-error.md)返回的值相同。

<a href="" id="ifhcinoctets"></a>**ifHCInOctets**  
接收定向的字节计数、接收-多播字节数和接收广播字节数的总和。 此总和与[OID\_代\_字节\_RCV](oid-gen-bytes-rcv.md)返回的值相同。

<a href="" id="ifhcinucastpkts"></a>**ifHCInUcastPkts**  
收到但未发生错误的定向数据包的数量。 此数字与[OID\_代\_\_RCV 返回\_帧](oid-gen-directed-frames-rcv.md)的值相同。

<a href="" id="ifhcinmulticastpkts"></a>**ifHCInMulticastPkts**  
接收的无错误的多播/功能数据包的数目。 此数值与[OID\_代\_多播\_帧\_RCV](oid-gen-multicast-frames-rcv.md)返回的值相同。

<a href="" id="ifhcinbroadcastpkts"></a>**ifHCInBroadcastPkts**  
接收时未出现错误的广播数据包的数量。 此数字与[OID\_代\_广播\_帧\_RCV](oid-gen-broadcast-frames-rcv.md)返回的值相同。

<a href="" id="ifhcoutoctets"></a>**ifHCOutOctets**  
传输-定向字节计数、传输-多播字节计数和传输广播字节计数的总和。 此总和与[OID\_代\_字节\_XMIT](oid-gen-bytes-xmit.md)返回的值相同。

<a href="" id="ifhcoutucastpkts"></a>**ifHCOutUcastPkts**  
传输没有错误的定向数据包的数量。 此数字与[OID\_代\_\_XMIT 返回\_帧](oid-gen-directed-frames-xmit.md)的值相同。

<a href="" id="ifhcoutmulticastpkts"></a>**ifHCOutMulticastPkts**  
传输没有错误的多播/功能数据包的数量。 此数值与[OID\_代\_多播\_帧\_XMIT](oid-gen-multicast-frames-xmit.md)返回的值相同。

<a href="" id="ifhcoutbroadcastpkts"></a>**ifHCOutBroadcastPkts**  
传输没有错误的广播数据包的数量。 此数字与[OID\_代\_广播\_帧\_XMIT](oid-gen-broadcast-frames-xmit.md)返回的值相同。

<a href="" id="ifouterrors"></a>**ifOutErrors**  
传输错误计数。 此计数与[OID\_代\_XMIT\_错误](oid-gen-xmit-error.md)返回的值相同。

<a href="" id="ifoutdiscards"></a>**ifOutDiscards**  
接口丢弃的数据包数。 这与通过查询[oid\_GEN\_XMIT\_放弃](oid-gen-xmit-discards.md)oid）返回的值相同。

<a href="" id="ifhcinucastoctets"></a>**ifHCInUcastOctets**  
接收到的未出现错误的定向数据包中的字节数。 此计数与[OID\_代\_定向\_字节\_RCV](oid-gen-directed-bytes-rcv.md)返回的值相同。

<a href="" id="ifhcinmulticastoctets"></a>**ifHCInMulticastOctets**  
在未发生错误的情况下接收的多播/功能数据包中的字节数。 此计数与[OID\_代\_多播\_字节\_RCV](oid-gen-multicast-bytes-rcv.md)返回的值相同。

<a href="" id="ifhcinbroadcastoctets"></a>**ifHCInBroadcastOctets**  
在未发生错误的情况下接收的广播数据包中的字节数。 此计数与[OID\_代\_广播\_字节\_RCV](oid-gen-broadcast-bytes-rcv.md)返回的值相同。

<a href="" id="ifhcoutucastoctets"></a>**ifHCOutUcastOctets**  
定向数据包中传输的字节数，不包括错误。 此计数与[OID\_代\_定向\_字节\_XMIT](oid-gen-directed-bytes-xmit.md)返回的值相同。

<a href="" id="ifhcoutmulticastoctets"></a>**ifHCOutMulticastOctets**  
多播/函数数据包中传输的字节数，不包括错误。 此计数与[OID\_代\_多播\_字节\_XMIT](oid-gen-multicast-bytes-xmit.md)返回的值相同。

<a href="" id="ifhcoutbroadcastoctets"></a>**ifHCOutBroadcastOctets**  
广播数据包中传输的字节数，不包括错误。 此计数与[OID\_代\_广播\_字节\_XMIT](oid-gen-broadcast-bytes-xmit.md)返回的值相同。

<a name="remarks"></a>备注
-------

微型端口驱动程序必须实施统计信息计数器，并报告正确的统计信息值。 统计信息计数器是未签名的64位值。 微型端口驱动程序在 NDIS\_统计信息\_信息结构中返回统计信息。

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


[ **\_标头的 NDIS\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)

[OID\_代\_广播\_字节\_RCV](oid-gen-broadcast-bytes-rcv.md)

[OID\_代\_广播\_字节\_XMIT](oid-gen-broadcast-bytes-xmit.md)

[OID\_代\_广播\_帧\_RCV](oid-gen-broadcast-frames-rcv.md)

[OID\_代\_广播\_帧\_XMIT](oid-gen-broadcast-frames-xmit.md)

[OID\_代\_字节\_RCV](oid-gen-bytes-rcv.md)

[OID\_代\_字节\_XMIT](oid-gen-bytes-xmit.md)

[OID\_代\_定向\_字节\_RCV](oid-gen-directed-bytes-rcv.md)

[OID\_代\_定向\_字节\_XMIT](oid-gen-directed-bytes-xmit.md)

[OID\_代\_定向\_帧\_RCV](oid-gen-directed-frames-rcv.md)

[OID\_代\_定向\_帧\_XMIT](oid-gen-directed-frames-xmit.md)

[OID\_代\_多播\_帧\_RCV](oid-gen-multicast-frames-rcv.md)

[OID\_代\_多播\_帧\_XMIT](oid-gen-multicast-frames-xmit.md)

[OID\_代\_多播\_字节\_RCV](oid-gen-multicast-bytes-rcv.md)

[OID\_代\_多播\_字节\_XMIT](oid-gen-multicast-bytes-xmit.md)

[OID\_代\_RCV\_放弃](oid-gen-rcv-discards.md)

[OID\_GEN\_RCV\_错误](oid-gen-rcv-error.md)

[OID\_代\_XMIT\_放弃](oid-gen-xmit-discards.md)

[OID\_GEN\_XMIT\_错误](oid-gen-xmit-error.md)








