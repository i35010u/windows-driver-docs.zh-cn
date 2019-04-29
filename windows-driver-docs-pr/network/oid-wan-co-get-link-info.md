---
title: OID_WAN_CO_GET_LINK_INFO
description: OID_WAN_CO_GET_LINK_INFO OID 请求微型端口驱动程序，以返回有关当前状态的虚拟连接 (VC) 的 PPP 帧信息。 按如下所示定义 NDIS_WAN_CO_GET_LINK_INFO 结构中返回此信息。
ms.assetid: 26582bc4-c32f-4243-a208-9230c62f4d16
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WAN_CO_GET_LINK_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9700321d6e839163462b7b06d9dacc00be4f23df
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390662"
---
# <a name="oidwancogetlinkinfo"></a>OID\_WAN\_CO\_GET\_LINK\_INFO


OID\_WAN\_共同\_获取\_链接\_信息 OID 请求微型端口驱动程序，以返回有关当前状态的虚拟连接 (VC) 的 PPP 帧信息。 此信息返回在 NDIS\_WAN\_共同\_获取\_链接\_定义，如下所示的信息结构。

```ManagedCPlusPlus
    typedef struct _NDIS_WAN_CO_GET_LINK_INFO {
         OUT ULONG MaxSendFrameSize;
         OUT ULONG MaxRecvFrameSize;
         OUT ULONG SendFramingBits;
         OUT ULONG RecvFramingBits;
         OUT ULONG SendCompressionBits;
         OUT ULONG RecvCompressionBits;
         OUT ULONG SendACCM;
         OUT ULONG RecvACCM;
    } NDIS_WAN_CO_GET_LINK_INFO,   *PNDIS_WAN_CO_GET_LINK_INFO;
```




此结构的成员包含下列信息：

<a href="" id="maxsendframesize"></a>**MaxSendFrameSize**  
指定最大缓冲区大小，以字节为单位，微型端口驱动程序可以接受此 VC 上传输。 微型端口驱动程序*MiniportCoSendPackets*函数可以拒绝任何传入的发送数据包的大小超出此大小。

<a href="" id="maxrecvframesize"></a>**MaxRecvFrameSize**  
指定将从网络接收的最大数据包。 微型端口驱动程序可以删除任何较大的数据包。

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
对于异步媒体类型，逻辑位 0-31 指示要将字节塞得满满的相应字节。 也就是说，如果位 0 设置为 1，然后 ASCII 字符 0x00 应是字节塞得满满，等等。

<a href="" id="recvaccm"></a>**RecvACCM**  
对于所述**SendACCM**。

<a name="remarks"></a>备注
-------

可能的值**SendFramingBits**并**RecvFramingBits**包括驱动程序到该 OID 的响应中返回任何\_WAN\_共同\_获取\_链接\_信息查询。

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


[OID\_WAN\_CO\_GET\_LINK\_INFO](oid-wan-co-get-link-info.md)








