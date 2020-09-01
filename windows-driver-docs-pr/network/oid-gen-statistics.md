---
title: OID_GEN_STATISTICS
description: 作为查询，NDIS 和过量驱动程序使用 OID_GEN_STATISTICS OID 获取适配器或微型端口驱动程序的统计信息。
ms.assetid: ff81d6b0-806d-4ddf-9da1-a169221be61f
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_STATISTICS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 49d4e2dc72c847053b882da0eef109650fd370e0
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210129"
---
# <a name="oid_gen_statistics"></a>OID \_ 生成 \_ 统计信息


作为查询，NDIS 和过量驱动程序使用 OID \_ GEN \_ STATISTICS OID 获取适配器或微型端口驱动程序的统计信息。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
必需。

NDIS \_ 统计 \_ 信息结构定义如下：

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
NDIS 统计信息结构的 [**ndis \_ 对象 \_ 标头**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header) 结构 \_ \_ 。 设置**标头**指定为 ndis 对象类型默认值的结构的**类型**成员 \_ \_ \_ 、Ndis 统计信息修订版本1的**修订**成员， \_ \_ \_ \_ 以及 ndis **Size** \_ SIZEOF \_ 统计 \_ 信息 \_ 修订版 \_ 1 的大小成员。

<a href="" id="supportedstatistics"></a>**SupportedStatistics**  
微型端口驱动程序支持的统计信息集。

**注意**  NDIS 6.0 和更高版本的驱动程序必须支持所有统计信息，并且在查询 OID 生成统计信息时必须报告它们 \_ \_ 。



该值是以下标志的按位 "或"：

<a href="" id="ndis-statistics-flags-valid-directed-frames-rcv"></a>NDIS \_ 统计信息 \_ 标志 \_ 有效 \_ 定向 \_ 帧 \_ RCV  
**IfHCInUcastPkts**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-multicast-frames-rcv"></a>NDIS \_ 统计信息 \_ 标志 \_ 有效的 \_ 多播 \_ 帧 \_ RCV  
**IfHCInMulticastPkts**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-broadcast-frames-rcv"></a>NDIS \_ 统计信息 \_ 标志 \_ 有效的 \_ 广播 \_ 帧 \_ RCV  
**IfHCInBroadcastPkts**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-bytes-rcv"></a>NDIS \_ STATISTICS \_ 标志 \_ 有效 \_ 字节 \_ RCV  
**IfHCInOctets**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-rcv-discards"></a>NDIS \_ STATISTICS \_ 标志 \_ 有效的 \_ RCV \_ 放弃  
**IfInDiscards**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-rcv-error"></a>NDIS \_ STATISTICS \_ 标志 \_ 有效的 \_ RCV \_ 错误  
**IfInErrors**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-directed-frames-xmit"></a>NDIS \_ 统计信息 \_ 标志 \_ 有效 \_ 定向 \_ 帧 \_ XMIT  
**IfHCOutUcastPkts**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-multicast-frames-xmit"></a>NDIS \_ 统计信息 \_ 标志 \_ 有效的 \_ 多播 \_ 帧 \_ XMIT  
**IfHCOutMulticastPkts**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-broadcast-frames-xmit"></a>NDIS \_ 统计信息 \_ 标志 \_ 有效的 \_ 广播 \_ 帧 \_ XMIT  
**IfHCOutBroadcastPkts**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-bytes-xmit"></a>NDIS \_ STATISTICS \_ 标志 \_ 有效 \_ 字节 \_ XMIT  
**IfHCOutOctets**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-xmit-error"></a>NDIS \_ STATISTICS \_ 标志 \_ 有效的 \_ XMIT \_ 错误  
**IfOutErrors**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-xmit-discards"></a>NDIS \_ STATISTICS \_ 标志 \_ 有效的 \_ XMIT \_ 放弃  
**IfOutDiscards**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-directed-bytes-rcv"></a>NDIS \_ STATISTICS \_ 标志 \_ 有效 \_ 定向 \_ 字节 \_ RCV  
**IfHCInUcastOctets**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-multicast-bytes-rcv"></a>NDIS \_ STATISTICS \_ 标志 \_ 有效的 \_ 多播 \_ 字节 \_ RCV  
**IfHCInMulticastOctets**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-broadcast-bytes-rcv"></a>NDIS \_ STATISTICS \_ 标志 \_ 有效的 \_ 广播 \_ 字节 \_ RCV  
**IfHCInBroadcastOctets**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-directed-bytes-xmit"></a>NDIS \_ STATISTICS \_ 标志 \_ 有效 \_ 定向 \_ 字节 \_ XMIT  
**IfHCOutUcastOctets**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-multicast-bytes-xmit"></a>NDIS \_ STATISTICS \_ 标志 \_ 有效的 \_ 多播 \_ 字节 \_ XMIT  
**IfHCOutMulticastOctets**成员中的数据是有效的。

<a href="" id="ndis-statistics-flags-valid-broadcast-bytes-xmit"></a>NDIS \_ STATISTICS \_ 标志 \_ 有效的 \_ 广播 \_ 字节 \_ XMIT  
**IfHCOutBroadcastOctets**成员中的数据是有效的。

<a href="" id="ifindiscards"></a>**ifInDiscards**  
丢弃的接收缓冲区错误计数。 此值与 [OID 生成 \_ \_ RCV \_ 放弃](oid-gen-rcv-discards.md) 的值相同。

<a href="" id="ifinerrors"></a>**ifInErrors**  
接收错误计数。 此计数与 [OID 生成 \_ \_ RCV \_ 错误](oid-gen-rcv-error.md) 返回的值相同。

<a href="" id="ifhcinoctets"></a>**ifHCInOctets**  
接收定向的字节计数、接收-多播字节数和接收广播字节数的总和。 此总和与 [OID 生成 \_ \_ 字节 \_ RCV](oid-gen-bytes-rcv.md) 返回的值相同。

<a href="" id="ifhcinucastpkts"></a>**ifHCInUcastPkts**  
收到但未发生错误的定向数据包的数量。 此数字与 [OID 生成 \_ \_ 定向 \_ 帧 \_ RCV](oid-gen-directed-frames-rcv.md) 返回的值相同。

<a href="" id="ifhcinmulticastpkts"></a>**ifHCInMulticastPkts**  
接收的无错误的多播/功能数据包的数目。 此数字与 [OID 生成 \_ \_ 多播 \_ 帧 \_ RCV](oid-gen-multicast-frames-rcv.md) 返回的值相同。

<a href="" id="ifhcinbroadcastpkts"></a>**ifHCInBroadcastPkts**  
接收时未出现错误的广播数据包的数量。 此数字与 [OID 生成 \_ \_ 广播 \_ 帧 \_ RCV](oid-gen-broadcast-frames-rcv.md) 返回的值相同。

<a href="" id="ifhcoutoctets"></a>**ifHCOutOctets**  
传输-定向字节计数、传输-多播字节计数和传输广播字节计数的总和。 此总和与 [OID 生成 \_ \_ 字节 \_ XMIT](oid-gen-bytes-xmit.md) 返回的值相同。

<a href="" id="ifhcoutucastpkts"></a>**ifHCOutUcastPkts**  
传输没有错误的定向数据包的数量。 此数字与 [OID 生成 \_ \_ 定向 \_ 帧 \_ XMIT](oid-gen-directed-frames-xmit.md) 返回的值相同。

<a href="" id="ifhcoutmulticastpkts"></a>**ifHCOutMulticastPkts**  
传输没有错误的多播/功能数据包的数量。 此数字与 [OID 生成 \_ \_ 多播 \_ 帧 \_ XMIT](oid-gen-multicast-frames-xmit.md) 返回的值相同。

<a href="" id="ifhcoutbroadcastpkts"></a>**ifHCOutBroadcastPkts**  
传输没有错误的广播数据包的数量。 此数字与 [OID 生成 \_ \_ 广播 \_ 帧 \_ XMIT](oid-gen-broadcast-frames-xmit.md) 返回的值相同。

<a href="" id="ifouterrors"></a>**ifOutErrors**  
传输错误计数。 此计数与 [OID 生成 \_ \_ XMIT \_ 错误](oid-gen-xmit-error.md) 返回的值相同。

<a href="" id="ifoutdiscards"></a>**ifOutDiscards**  
接口丢弃的数据包数。 这与通过查询 [oid \_ GEN \_ XMIT \_ 丢弃](oid-gen-xmit-discards.md) oid 返回的值相同。

<a href="" id="ifhcinucastoctets"></a>**ifHCInUcastOctets**  
接收到的未出现错误的定向数据包中的字节数。 此计数与 [OID 生成 \_ \_ 定向 \_ 字节 \_ RCV](oid-gen-directed-bytes-rcv.md) 返回的值相同。

<a href="" id="ifhcinmulticastoctets"></a>**ifHCInMulticastOctets**  
在未发生错误的情况下接收的多播/功能数据包中的字节数。 此计数与 [OID 生成 \_ \_ 多播 \_ 字节 \_ RCV](oid-gen-multicast-bytes-rcv.md) 返回的值相同。

<a href="" id="ifhcinbroadcastoctets"></a>**ifHCInBroadcastOctets**  
在未发生错误的情况下接收的广播数据包中的字节数。 此计数与 [OID 生成 \_ \_ 广播 \_ 字节 \_ RCV](oid-gen-broadcast-bytes-rcv.md) 返回的值相同。

<a href="" id="ifhcoutucastoctets"></a>**ifHCOutUcastOctets**  
定向数据包中传输的字节数，不包括错误。 此计数与 [OID 生成 \_ \_ 定向 \_ 字节 \_ XMIT](oid-gen-directed-bytes-xmit.md) 返回的值相同。

<a href="" id="ifhcoutmulticastoctets"></a>**ifHCOutMulticastOctets**  
多播/函数数据包中传输的字节数，不包括错误。 此计数与 [OID 生成 \_ \_ 多播 \_ 字节 \_ XMIT](oid-gen-multicast-bytes-xmit.md) 返回的值相同。

<a href="" id="ifhcoutbroadcastoctets"></a>**ifHCOutBroadcastOctets**  
广播数据包中传输的字节数，不包括错误。 此计数与 [OID 生成 \_ \_ 广播 \_ 字节 \_ XMIT](oid-gen-broadcast-bytes-xmit.md) 返回的值相同。

<a name="remarks"></a>备注
-------

微型端口驱动程序必须实施统计信息计数器，并报告正确的统计信息值。 统计信息计数器是未签名的64位值。 微型端口驱动程序返回 NDIS \_ 统计信息结构中的统计信息 \_ 。

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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS \_ 对象 \_ 标头**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)

[OID \_ 生成 \_ 广播 \_ 字节 \_ RCV](oid-gen-broadcast-bytes-rcv.md)

[OID \_ 生成 \_ 广播 \_ 字节 \_ XMIT](oid-gen-broadcast-bytes-xmit.md)

[OID \_ 生成 \_ 广播 \_ 帧 \_ RCV](oid-gen-broadcast-frames-rcv.md)

[OID \_ 生成 \_ 广播 \_ 帧 \_ XMIT](oid-gen-broadcast-frames-xmit.md)

[OID \_ GEN \_ BYTES \_ RCV](oid-gen-bytes-rcv.md)

[OID \_ GEN \_ BYTES \_ XMIT](oid-gen-bytes-xmit.md)

[OID \_ 生成 \_ 定向 \_ 字节 \_ RCV](oid-gen-directed-bytes-rcv.md)

[OID \_ 生成 \_ 定向 \_ 字节 \_ XMIT](oid-gen-directed-bytes-xmit.md)

[OID \_ 生成 \_ 定向 \_ 帧 \_ RCV](oid-gen-directed-frames-rcv.md)

[OID \_ 生成 \_ 定向 \_ 帧 \_ XMIT](oid-gen-directed-frames-xmit.md)

[OID \_ 生成 \_ 多播 \_ 帧 \_ RCV](oid-gen-multicast-frames-rcv.md)

[OID \_ 生成 \_ 多播 \_ 帧 \_ XMIT](oid-gen-multicast-frames-xmit.md)

[OID \_ 生成 \_ 多播 \_ 字节 \_ RCV](oid-gen-multicast-bytes-rcv.md)

[OID \_ 生成 \_ 多播 \_ 字节 \_ XMIT](oid-gen-multicast-bytes-xmit.md)

[OID \_ 生成 \_ RCV \_ 放弃](oid-gen-rcv-discards.md)

[OID \_ 生成 \_ RCV \_ 错误](oid-gen-rcv-error.md)

[OID \_ 生成 \_ XMIT \_ 放弃](oid-gen-xmit-discards.md)

[OID \_ 生成 \_ XMIT \_ 错误](oid-gen-xmit-error.md)