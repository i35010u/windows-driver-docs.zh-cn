---
title: OID_GEN_STATISTICS
description: 为查询，NDIS 和基础驱动程序使用 OID_GEN_STATISTICS OID 来获取统计信息的适配器或微型端口驱动程序。
ms.assetid: ff81d6b0-806d-4ddf-9da1-a169221be61f
ms.date: 08/08/2017
keywords: -OID_GEN_STATISTICS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 059e96534bcb16c0958a0a0ea1e631c86dd39a0e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387000"
---
# <a name="oidgenstatistics"></a>OID\_常规\_统计信息


为查询，NDIS 和基础驱动程序使用 OID\_常规\_统计信息 OID，若要获取的适配器或微型端口驱动程序统计信息。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
必需。

NDIS\_统计信息\_信息结构定义，如下所示：

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
[ **NDIS\_对象\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_object_header) ndis 结构\_统计信息\_信息结构。 设置**类型**结构中的成员的**标头**指定到 NDIS\_对象\_类型\_默认情况下，**修订**成员添加到 NDIS\_统计信息\_信息\_修订\_1，并且**大小**成员添加到 NDIS\_SIZEOF\_统计信息\_INFO\_修订\_1。

<a href="" id="supportedstatistics"></a>**SupportedStatistics**  
微型端口驱动程序支持的统计信息集。

**请注意**NDIS 6.0 和更高版本的驱动程序必须支持的所有统计信息并在必须报告这些查询的 OID 时\_代\_统计信息。



值为下列标志的按位 OR:

<a href="" id="ndis-statistics-flags-valid-directed-frames-rcv"></a>NDIS\_统计信息\_标志\_有效\_定向\_帧\_RCV  
中的数据**ifHCInUcastPkts**成员是否有效。

<a href="" id="ndis-statistics-flags-valid-multicast-frames-rcv"></a>NDIS\_统计信息\_标志\_有效\_多播\_帧\_RCV  
中的数据**ifHCInMulticastPkts**成员是否有效。

<a href="" id="ndis-statistics-flags-valid-broadcast-frames-rcv"></a>NDIS\_STATISTICS\_FLAGS\_VALID\_BROADCAST\_FRAMES\_RCV  
中的数据**ifHCInBroadcastPkts**成员是否有效。

<a href="" id="ndis-statistics-flags-valid-bytes-rcv"></a>NDIS\_STATISTICS\_FLAGS\_VALID\_BYTES\_RCV  
中的数据**ifHCInOctets**成员是否有效。

<a href="" id="ndis-statistics-flags-valid-rcv-discards"></a>NDIS\_STATISTICS\_FLAGS\_VALID\_RCV\_DISCARDS  
中的数据**ifInDiscards**成员是否有效。

<a href="" id="ndis-statistics-flags-valid-rcv-error"></a>NDIS\_STATISTICS\_FLAGS\_VALID\_RCV\_ERROR  
中的数据**ifInErrors**成员是否有效。

<a href="" id="ndis-statistics-flags-valid-directed-frames-xmit"></a>NDIS\_统计信息\_标志\_有效\_定向\_帧\_XMIT  
中的数据**ifHCOutUcastPkts**成员是否有效。

<a href="" id="ndis-statistics-flags-valid-multicast-frames-xmit"></a>NDIS\_统计信息\_标志\_有效\_多播\_帧\_XMIT  
中的数据**ifHCOutMulticastPkts**成员是否有效。

<a href="" id="ndis-statistics-flags-valid-broadcast-frames-xmit"></a>NDIS\_STATISTICS\_FLAGS\_VALID\_BROADCAST\_FRAMES\_XMIT  
中的数据**ifHCOutBroadcastPkts**成员是否有效。

<a href="" id="ndis-statistics-flags-valid-bytes-xmit"></a>NDIS\_统计信息\_标志\_有效\_字节\_XMIT  
中的数据**ifHCOutOctets**成员是否有效。

<a href="" id="ndis-statistics-flags-valid-xmit-error"></a>NDIS\_统计信息\_标志\_有效\_XMIT\_错误  
中的数据**ifOutErrors**成员是否有效。

<a href="" id="ndis-statistics-flags-valid-xmit-discards"></a>NDIS\_统计信息\_标志\_有效\_XMIT\_放弃  
中的数据**ifOutDiscards**成员是否有效。

<a href="" id="ndis-statistics-flags-valid-directed-bytes-rcv"></a>NDIS\_统计信息\_标志\_有效\_定向\_字节\_RCV  
中的数据**ifHCInUcastOctets**成员是否有效。

<a href="" id="ndis-statistics-flags-valid-multicast-bytes-rcv"></a>NDIS\_统计信息\_标志\_有效\_多播\_字节\_RCV  
中的数据**ifHCInMulticastOctets**成员是否有效。

<a href="" id="ndis-statistics-flags-valid-broadcast-bytes-rcv"></a>NDIS\_STATISTICS\_FLAGS\_VALID\_BROADCAST\_BYTES\_RCV  
中的数据**ifHCInBroadcastOctets**成员是否有效。

<a href="" id="ndis-statistics-flags-valid-directed-bytes-xmit"></a>NDIS\_统计信息\_标志\_有效\_定向\_字节\_XMIT  
中的数据**ifHCOutUcastOctets**成员是否有效。

<a href="" id="ndis-statistics-flags-valid-multicast-bytes-xmit"></a>NDIS\_统计信息\_标志\_有效\_多播\_字节\_XMIT  
中的数据**ifHCOutMulticastOctets**成员是否有效。

<a href="" id="ndis-statistics-flags-valid-broadcast-bytes-xmit"></a>NDIS\_STATISTICS\_FLAGS\_VALID\_BROADCAST\_BYTES\_XMIT  
中的数据**ifHCOutBroadcastOctets**成员是否有效。

<a href="" id="ifindiscards"></a>**ifInDiscards**  
删除-接收-缓冲区错误计数。 这是相同的值，该值[OID\_代\_RCV\_放弃](oid-gen-rcv-discards.md)返回。

<a href="" id="ifinerrors"></a>**ifInErrors**  
接收错误计数。 此计数是相同的值的[OID\_代\_RCV\_错误](oid-gen-rcv-error.md)返回。

<a href="" id="ifhcinoctets"></a>**ifHCInOctets**  
定向接收的字节数、 接收多播字节数和接收广播字节数之和。 此总和是相同的值的[OID\_代\_字节\_RCV](oid-gen-bytes-rcv.md)返回。

<a href="" id="ifhcinucastpkts"></a>**ifHCInUcastPkts**  
定向无错误收到的数据包数。 此数字是相同的值的[OID\_代\_定向\_帧\_RCV](oid-gen-directed-frames-rcv.md)返回。

<a href="" id="ifhcinmulticastpkts"></a>**ifHCInMulticastPkts**  
多播/功能未出现错误接收的数据包数。 此数字是相同的值的[OID\_代\_多播\_帧\_RCV](oid-gen-multicast-frames-rcv.md)返回。

<a href="" id="ifhcinbroadcastpkts"></a>**ifHCInBroadcastPkts**  
接收未出现错误的广播数据包数。 此数字是相同的值的[OID\_代\_广播\_帧\_RCV](oid-gen-broadcast-frames-rcv.md)返回。

<a href="" id="ifhcoutoctets"></a>**ifHCOutOctets**  
定向传输的字节数、 传输多播字节数和传输广播字节数之和。 此总和是相同的值的[OID\_代\_字节\_XMIT](oid-gen-bytes-xmit.md)返回。

<a href="" id="ifhcoutucastpkts"></a>**ifHCOutUcastPkts**  
没有错误传输的定向数据包数。 此数字是相同的值的[OID\_代\_定向\_帧\_XMIT](oid-gen-directed-frames-xmit.md)返回。

<a href="" id="ifhcoutmulticastpkts"></a>**ifHCOutMulticastPkts**  
没有错误传输的多播功能/数据包数。 此数字是相同的值的[OID\_代\_多播\_帧\_XMIT](oid-gen-multicast-frames-xmit.md)返回。

<a href="" id="ifhcoutbroadcastpkts"></a>**ifHCOutBroadcastPkts**  
没有错误传输的广播数据包数。 此数字是相同的值的[OID\_代\_广播\_帧\_XMIT](oid-gen-broadcast-frames-xmit.md)返回。

<a href="" id="ifouterrors"></a>**ifOutErrors**  
传输错误计数。 此计数是相同的值的[OID\_代\_XMIT\_错误](oid-gen-xmit-error.md)返回。

<a href="" id="ifoutdiscards"></a>**ifOutDiscards**  
由接口将被丢弃的数据包数。 这是通过查询返回的值与相同[OID\_代\_XMIT\_放弃](oid-gen-xmit-discards.md)OID。

<a href="" id="ifhcinucastoctets"></a>**ifHCInUcastOctets**  
定向无错误收到的数据包中的字节数。 此计数是相同的值的[OID\_代\_定向\_字节\_RCV](oid-gen-directed-bytes-rcv.md)返回。

<a href="" id="ifhcinmulticastoctets"></a>**ifHCInMulticastOctets**  
多播/功能未出现错误接收的数据包中的字节数。 此计数是相同的值的[OID\_代\_多播\_字节\_RCV](oid-gen-multicast-bytes-rcv.md)返回。

<a href="" id="ifhcinbroadcastoctets"></a>**ifHCInBroadcastOctets**  
接收未出现错误的广播数据包中的字节数。 此计数是相同的值的[OID\_代\_广播\_字节\_RCV](oid-gen-broadcast-bytes-rcv.md)返回。

<a href="" id="ifhcoutucastoctets"></a>**ifHCOutUcastOctets**  
没有错误传输的定向数据包中的字节数。 此计数是相同的值的[OID\_代\_定向\_字节\_XMIT](oid-gen-directed-bytes-xmit.md)返回。

<a href="" id="ifhcoutmulticastoctets"></a>**ifHCOutMulticastOctets**  
没有错误传输的多播功能/数据包中的字节数。 此计数是相同的值的[OID\_代\_多播\_字节\_XMIT](oid-gen-multicast-bytes-xmit.md)返回。

<a href="" id="ifhcoutbroadcastoctets"></a>**ifHCOutBroadcastOctets**  
没有错误传输的广播数据包中的字节数。 此计数是相同的值的[OID\_代\_广播\_字节\_XMIT](oid-gen-broadcast-bytes-xmit.md)返回。

<a name="remarks"></a>备注
-------

微型端口驱动程序必须实现的统计信息计数器和报告正确的统计信息值。 统计信息计数器是无符号的 64 位值。 微型端口驱动程序在 NDIS 中返回的统计信息\_统计信息\_信息结构。

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


[**NDIS\_对象\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_object_header)

[OID\_GEN\_BROADCAST\_BYTES\_RCV](oid-gen-broadcast-bytes-rcv.md)

[OID\_GEN\_BROADCAST\_BYTES\_XMIT](oid-gen-broadcast-bytes-xmit.md)

[OID\_GEN\_BROADCAST\_FRAMES\_RCV](oid-gen-broadcast-frames-rcv.md)

[OID\_GEN\_BROADCAST\_FRAMES\_XMIT](oid-gen-broadcast-frames-xmit.md)

[OID\_GEN\_BYTES\_RCV](oid-gen-bytes-rcv.md)

[OID\_GEN\_BYTES\_XMIT](oid-gen-bytes-xmit.md)

[OID\_GEN\_DIRECTED\_BYTES\_RCV](oid-gen-directed-bytes-rcv.md)

[OID\_GEN\_DIRECTED\_BYTES\_XMIT](oid-gen-directed-bytes-xmit.md)

[OID\_GEN\_DIRECTED\_FRAMES\_RCV](oid-gen-directed-frames-rcv.md)

[OID\_GEN\_DIRECTED\_FRAMES\_XMIT](oid-gen-directed-frames-xmit.md)

[OID\_GEN\_MULTICAST\_FRAMES\_RCV](oid-gen-multicast-frames-rcv.md)

[OID\_GEN\_MULTICAST\_FRAMES\_XMIT](oid-gen-multicast-frames-xmit.md)

[OID\_GEN\_MULTICAST\_BYTES\_RCV](oid-gen-multicast-bytes-rcv.md)

[OID\_GEN\_MULTICAST\_BYTES\_XMIT](oid-gen-multicast-bytes-xmit.md)

[OID\_GEN\_RCV\_DISCARDS](oid-gen-rcv-discards.md)

[OID\_GEN\_RCV\_ERROR](oid-gen-rcv-error.md)

[OID\_GEN\_XMIT\_DISCARDS](oid-gen-xmit-discards.md)

[OID\_GEN\_XMIT\_ERROR](oid-gen-xmit-error.md)








