---
title: OID_WAN_CO_SET_LINK_INFO
description: OID_WAN_CO_SET_LINK_INFO OID 请求微型端口驱动程序，可设置特定的虚拟连接 (VC) 的 PPP 帧信息。 一种协议使用 NDIS_WAN_CO_SET_LINK_INFO 结构，定义，如下所示，以指示此 PPP 帧信息。
ms.assetid: 4487289a-01f6-4ae1-b660-3011d66acb29
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WAN_CO_SET_LINK_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 0fada7f6db4ff5dc8e7ac56302de940f32a2fb1c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384631"
---
# <a name="oidwancosetlinkinfo"></a>OID\_WAN\_共同\_设置\_链接\_信息


OID\_WAN\_共同\_设置\_链接\_信息 OID 请求微型端口驱动程序，可设置特定的虚拟连接 (VC) 的 PPP 帧信息。 一种协议使用 NDIS\_WAN\_共同\_设置\_链接\_信息结构，定义，如下所示，以指示此 PPP 帧信息。

```ManagedCPlusPlus
    typedef struct _NDIS_WAN_CO_SET_LINK_INFO {
         IN ULONG MaxSendFrameSize;
         IN ULONG MaxRecvFrameSize;
         IN ULONG SendFramingBits;
         IN ULONG RecvFramingBits;
         IN ULONG SendCompressionBits;
         IN ULONG RecvCompressionBits;
         IN ULONG SendACCM;
         IN ULONG RecvACCM;
    } NDIS_WAN_CO_SET_LINK_INFO,   *PNDIS_WAN_CO_SET_LINK_INFO;
```




此结构的成员包含下列信息：

<a href="" id="maxsendframesize"></a>**MaxSendFrameSize**  
指定的最大缓冲区，以字节为单位，该协议将发送的此 VC。 此值必须小于或等于微型端口驱动程序返回[OID\_WAN\_共同\_获取\_链接\_信息](oid-wan-co-get-link-info.md)查询。

微型端口驱动程序*MiniportCoSendPackets*函数可以拒绝为此链接提交大于此值的任何发送数据包。

<a href="" id="maxrecvframesize"></a>**MaxRecvFrameSize**  
指定协议将随后接收的最大网络数据包。 此值必须小于或等于的微型端口驱动程序返回的 OID\_WAN\_共同\_获取\_链接\_信息查询。 微型端口驱动程序可以为此较大的 VC 删除任何已接收的数据包。

<a href="" id="sendframingbits"></a>**SendFramingBits**  
指定发送组帧位，指示应发送帧的类型。 如果微型端口驱动程序检测到不兼容性之间**SendFramingBits**并**RecvFramingBits**，它将返回 NDIS\_状态\_无效\_数据。

基于帧位适用应使用适当 NLPID 和组帧格式。

<a href="" id="recvframingbits"></a>**RecvFramingBits**  
指定接收组帧位，指示应接收的帧的类型。

<a href="" id="sendcompressionbits"></a>**SendCompressionBits**  
保留。

<a href="" id="recvcompressionbits"></a>**RecvCompressionBits**  
保留。

<a href="" id="sendaccm"></a>**SendACCM**  
对于异步媒体类型，逻辑位 0-31 指示要将字节塞得满满的相应字节。 也就是说，如果位 0 设置为一个然后 ASCII 字符 0x00 应是字节塞得满满，等等。

<a href="" id="recvaccm"></a>**RecvACCM**  
对于所述**SendACCM**。

<a name="remarks"></a>备注
-------

可能的值**SendFramingBits**并**RecvFramingBits**包括任何基础驱动程序在响应中返回[OID\_WAN\_共同\_获取\_信息](oid-wan-co-get-info.md)查询。

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
<td><p>支持 Windows Vista 中的 NDIS 6.0 和 NDIS 5.1 驱动程序。 支持 NDIS 5.1 在 Windows XP 中的驱动程序。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID\_WAN\_CO\_GET\_INFO](oid-wan-co-get-info.md)

[OID\_WAN\_CO\_GET\_LINK\_INFO](oid-wan-co-get-link-info.md)








