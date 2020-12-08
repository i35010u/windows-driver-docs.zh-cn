---
title: OID_WAN_CO_SET_LINK_INFO
description: OID_WAN_CO_SET_LINK_INFO OID 请求微型端口驱动程序设置特定虚拟连接的 PPP 帧信息 (VC) 。 协议使用如下定义的 NDIS_WAN_CO_SET_LINK_INFO 结构来指示此 PPP 帧信息。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WAN_CO_SET_LINK_INFO 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 38b56a39b02eb66aea92b29ba90a4758893f6ebd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839223"
---
# <a name="oid_wan_co_set_link_info"></a>OID \_ WAN \_ CO \_ 集 \_ 链接 \_ 信息


OID \_ WAN \_ CO \_ 集 \_ 链接 \_ 信息 OID 请求微型端口驱动程序设置特定虚拟连接的 PPP 帧信息 (VC) 。 协议使用 \_ 如下定义的 NDIS WAN \_ CO \_ 集 \_ 链接 \_ 信息结构来指示此 PPP 帧信息。

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




此结构的成员包含以下信息：

<a href="" id="maxsendframesize"></a>**MaxSendFrameSize**  
指定将为此 VC 发送的最大缓冲区（以字节为单位）。 此值必须小于或等于 [OID \_ WAN \_ CO \_ 获取 \_ 链接 \_ 信息](oid-wan-co-get-link-info.md) 查询的微型端口驱动程序返回的值。

微型端口驱动程序的 *MiniportCoSendPackets* 函数可以拒绝为大于此值的此链接提交的任何发送数据包。

<a href="" id="maxrecvframesize"></a>**MaxRecvFrameSize**  
指定协议随后将接收的最大网络数据包。 此值必须小于或等于 OID \_ WAN \_ CO \_ 获取 \_ 链接 \_ 信息查询的微型端口驱动程序返回的值。 微型端口驱动程序可以删除此 VC 的任何已接收的数据包。

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
对于异步媒体类型，逻辑位0-31 指示以字节剥制的相应字节。 也就是说，如果位0设置为 one，则 ASCII 字符0x00 应为 byte 剥制，依此类推。

<a href="" id="recvaccm"></a>**RecvACCM**  
如 **SendACCM** 所述。

<a name="remarks"></a>备注
-------

**SendFramingBits** 和 **RecvFramingBits** 的可能值包括为响应 [OID \_ WAN \_ CO \_ 获取 \_ 信息](oid-wan-co-get-info.md)查询而返回的任何基础驱动程序。

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


[OID \_ WAN \_ CO \_ 获取 \_ 信息](oid-wan-co-get-info.md)

[OID \_ WAN \_ CO \_ 获取 \_ 链接 \_ 信息](oid-wan-co-get-link-info.md)








