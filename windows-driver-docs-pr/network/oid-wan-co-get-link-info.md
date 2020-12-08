---
title: OID_WAN_CO_GET_LINK_INFO
description: OID_WAN_CO_GET_LINK_INFO OID 请求微型端口驱动程序返回有关虚拟连接的当前状态 (VC) 的 PPP 帧信息。 此信息以 NDIS_WAN_CO_GET_LINK_INFO 结构返回，如下所示。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WAN_CO_GET_LINK_INFO 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f7b2b552c66feac1907eb8c39ace440cf379331f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786041"
---
# <a name="oid_wan_co_get_link_info"></a>OID \_ WAN \_ CO \_ 获取 \_ 链接 \_ 信息


OID \_ WAN \_ CO \_ 获取 \_ 链接 \_ 信息 OID 请求微型端口驱动程序返回关于虚拟连接当前状态的 PPP 帧信息 (VC) 。 此信息将在 NDIS \_ WAN \_ CO \_ 获取 \_ 链接 \_ 信息结构中返回，如下所示。

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




此结构的成员包含以下信息：

<a href="" id="maxsendframesize"></a>**MaxSendFrameSize**  
指定微型端口驱动程序可用于在此 VC 上传输的最大缓冲区大小（以字节为单位）。 微型端口驱动程序的 *MiniportCoSendPackets* 函数可以拒绝大于此大小的任何传入发送数据包。

<a href="" id="maxrecvframesize"></a>**MaxRecvFrameSize**  
指定将从网络接收的最大数据包。 微型端口驱动程序可以删除更大的任何数据包。

<a href="" id="sendframingbits"></a>**SendFramingBits**  
指定发送组帧位，指示应发送的组帧类型。 如果微型端口驱动程序检测到 **SendFramingBits** 与 **RecvFramingBits** 之间的不兼容，则它会返回 NDIS \_ 状态 " \_ 无效 \_ 数据"。

应在适当的位置根据帧位使用正确的 NLPID 和组帧格式。

<a href="" id="recvframingbits"></a>**RecvFramingBits**  
指定接收帧的位，指示应接收的帧类型。

<a href="" id="sendcompressionbits"></a>**SendCompressionBits**  
保留。

<a href="" id="recvcompressionbits"></a>**RecvCompressionBits**  
保留。

<a href="" id="sendaccm"></a>**SendACCM**  
对于异步媒体类型，逻辑位0-31 指示以字节剥制的相应字节。 也就是说，如果位0设置为1，则 ASCII 字符0x00 应为 byte 剥制，依此类推。

<a href="" id="recvaccm"></a>**RecvACCM**  
如 **SendACCM** 所述。

<a name="remarks"></a>备注
-------

**SendFramingBits** 和 **RecvFramingBits** 的可能值包括为响应 OID \_ WAN \_ CO \_ 获取 \_ 链接 \_ 信息查询而返回的任何驱动程序。

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
<td><p>支持 Windows Vista 中的 NDIS 6.0 和 NDIS 5.1 驱动程序。 Windows XP 中的 NDIS 5.1 驱动程序支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID \_ WAN \_ CO \_ 获取 \_ 链接 \_ 信息](oid-wan-co-get-link-info.md)








