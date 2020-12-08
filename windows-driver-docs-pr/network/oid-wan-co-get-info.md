---
title: OID_WAN_CO_GET_INFO
description: OID_WAN_CO_GET_INFO OID 请求微型端口驱动程序返回适用于其 NIC 上 (VCs) 所有虚拟连接的信息。 此信息以 NDIS_WAN_CO_INFO 结构返回，如下所示。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WAN_CO_GET_INFO 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1573ca7ca1a2937b72ae6da26e9d3eeaac5e74a0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786045"
---
# <a name="oid_wan_co_get_info"></a>OID \_ WAN \_ CO \_ 获取 \_ 信息


OID \_ WAN \_ CO \_ 获取 \_ 信息 OID 请求微型端口驱动程序返回适用于其 NIC 上 (VCs) 的所有虚拟连接的信息。 此信息将在 NDIS \_ WAN \_ CO \_ 信息结构中返回，如下所示。

```ManagedCPlusPlus
    typedef struct _NDIS_WAN_CO_INFO {
         OUT ULONG MaxFrameSize;
         OUT ULONG MaxSendWindow;
         OUT ULONG FramingBits;
         OUT ULONG DesiredACCM;
    } NDIS_WAN_CO_INFO, *PNDIS_WAN_CO_INFO;
```




此结构的成员包含以下信息：

<a href="" id="maxframesize"></a>**Messagingfactorysettings.amqptransportsettings.maxframesize**  
指定微型端口驱动程序可发送和接收的任何网络包的最大帧大小。 此值应排除微型端口驱动程序自身的组帧开销和/或 PPP HDLC 开销。 此值通常约为1500。

但是，所有 CoNDIS WAN 微型端口驱动程序应使用比它们为此 OID 返回的值大32字节的内部 **messagingfactorysettings.amqptransportsettings.maxframesize** 。 例如，为此 OID 返回1500的 CoNDIS WAN 微型端口驱动程序在内部接受并发送到1532。 此类微型端口驱动程序可以随时支持未来的桥接和其他协议。

<a href="" id="maxsendwindow"></a>**MaxSendWindow**  
指定 CoNDIS WAN 微型端口驱动程序可以在 VC 上处理的未完成数据包的最大数量。 此成员必须设置为至少一个。

NDISWAN 驱动程序使用此成员的值来限制在 NDISWAN 保留发送数据包之前，它在向微型端口驱动程序的 *MiniportCoSendPackets* 函数发送请求时所提交的数据包数。 这些数据包将排队等候，直到微型端口驱动程序完成未完成的发送。 微型端口驱动程序可以使用微型端口驱动程序传递给 [**NdisMCoIndicateStatus**](/previous-versions/windows/hardware/network/ff553458(v=vs.85))的 [**WAN \_ CO \_ LINKPARAMS**](/previous-versions/windows/hardware/network/ff565819(v=vs.85))结构中的 **SendWindow** 成员，以动态方式和每个 VC 来调整此值。 NDISWAN 使用当前 **SendWindow** 值作为其未处理发送的限制。 如果微型端口驱动程序将 **SendWindow** 设置为零，则 NDISWAN 必须停止发送特定 VC 的数据包。 也就是说，微型端口驱动程序指定 "发送" 窗口已关闭，这实际上指定它不能接受来自 NDISWAN 的任何数据包。

由于 CoNDIS WAN 微型端口驱动程序必须在内部将数据包排队，因此 **MaxSendWindow** 的值理论上 **最大** ( ULONG) 。 但是，此驱动程序确定的值应反映 NIC 的链接速度或硬件功能。 例如，如果微型端口驱动程序的 NIC 始终具有至少四个数据包的空间，则微型端口驱动程序会将 **MaxSendWindow** 设置为4，以便可以将任何传入的 *MiniportCoSendPackets* 包立即放在硬件上。

<a href="" id="framingbits"></a>**FramingBits**  
一个32位值，指定一个指定微型端口驱动程序支持的组帧类型的位掩码。 微型端口驱动程序可以使用二进制或运算符指定下列值的组合：

<a href="" id="ras-framing"></a>RAS \_ 组帧  
仅当微型端口驱动程序可以检测到较旧的 RAS 帧时设置。 仅支持早期 RAS 帧的旧驱动程序设置此标志。

<a href="" id="ras-compression"></a>RAS \_ 压缩  
仅当微型端口驱动程序支持较旧的 RAS 压缩方案时才进行设置。

<a href="" id="ppp-framing"></a>PPP \_ 组帧  
应始终设置。 指示微型端口驱动程序可以检测并支持其媒体类型的 PPP 帧。

<a href="" id="ppp-compress-address-control"></a>PPP \_ 压缩 \_ 地址 \_ 控制  
设置微型端口驱动程序是否支持 PPP 地址和控制字段压缩。

如果协商了此 LCP 选项，NDISWAN 将删除地址和控制字段。 某些 WAN 中型类型（如 .25）不支持此选项。

<a href="" id="ppp-compress-protocol-field"></a>PPP \_ 压缩 \_ 协议 \_ 字段  
设置微型端口驱动程序是否支持 PPP 协议字段压缩。

如果此 LCP 选项已协商，NDISWAN 将从 "协议" 字段中删除一个字节。

<a href="" id="ppp-accm-supported"></a>\_支持 PPP ACCM \_  
设置微型端口驱动程序是否支持异步控制字符映射。 此位仅适用于异步媒体，如调制解调器。 如果设置此位， **DesiredACCM** 成员应是有效的。

<a href="" id="ppp-multilink-framing"></a>PPP \_ 多链路 \_ 帧  
如果微型端口驱动程序支持在 IETF RFC 1717 中指定的多链路帧，则设置。

<a href="" id="ppp-short-sequence-hdr-format"></a>PPP \_ 短 \_ 序列 \_ HDR \_ 格式  
如果微型端口驱动程序支持在 IETF RFC 1717 中指定的多链路帧的标头格式，则设置。

<a href="" id="slip-framing"></a>单 \_ 组帧  
设置微型端口驱动程序是否可以检测并支持 SLIP 组帧 (仅) 的异步微型端口驱动程序。

<a href="" id="slip-vj-compression"></a>SLIP \_ VJ \_ 压缩  
设置微型端口驱动程序是否可以支持 Van Jacobsen TCP/IP 标头压缩。 NDISWAN 支持 \_ \_) 有16个槽的 (的滑动 VJ 压缩。 支持单组帧的异步媒体 (串行微型端口驱动程序) 应设置此位。

异步媒体无需编写任何代码即可支持 VJ 标头压缩。 NDISWAN 将负责处理。

<a href="" id="slip-vj-autodetect"></a>SLIP \_ VJ 自动 \_ 检测  
设置微型端口驱动程序是否可以自动检测 Van Jacobsen TCP/IP 标头压缩。 NDISWAN 将自动检测 VJ 标头压缩。 异步媒体 (串行微型端口驱动程序) 如果支持单组帧，则应设置此位。

<a href="" id="tapi-provider"></a>TAPI \_ 提供程序  
设置微型端口驱动程序是否支持 TAPI 服务提供程序 Oid。 除非设置了此位，否则不会对微型端口驱动程序调用 TAPI OID。

<a href="" id="media-nrz-encoding"></a>媒体 \_ NRZ \_ 编码  
设置微型端口驱动程序是否支持 NRZ 编码，某些媒体类型（例如 ISDN）的 PPP 默认值。 保留此值供将来使用。

<a href="" id="media-nrzi-encoding"></a>媒体 \_ NRZI \_ 编码  
设置微型端口驱动程序是否支持 NRZI 编码。 保留此值供将来使用。

<a href="" id="media-nlpid"></a>媒体 \_ NLPID  
如果微型端口驱动程序具有并且可以在其框架中设置 NLPID，则设置。 保留此值供将来使用。

<a href="" id="rfc-1356-framing"></a>RFC \_ 1356 \_ 帧  
如果微型端口驱动程序支持 IETF RFC 1356 和 ISDN 组帧，则设置。 保留此值供将来使用。

<a href="" id="rfc-1483-framing"></a>RFC \_ 1483 \_ 帧  
设置微型端口驱动程序是否支持 IETF RFC 1483 ATM 适配第5层封装。 保留此值供将来使用。

<a href="" id="rfc-1490-framing"></a>RFC \_ 1490 \_ 帧  
如果微型端口驱动程序支持 IETF RFC 1490 帧中继帧，则设置。 保留此值供将来使用。

<a href="" id="nbf-preserve-mac-address"></a>NBF \_ 保留 \_ MAC \_ 地址  
设置微型端口驱动程序是否支持草稿 "PPP NETBIOS 帧控制协议 (NBFCP) " 中指定的 IETF 帧。

<a href="" id="shiva-framing"></a>SHIVA \_ 组帧  
由 NBF 取代 \_ \_ MAC \_ 地址。

<a href="" id="pass-through-mode"></a>传递 \_ \_ 模式  
设置微型端口驱动程序是否执行其自己的帧。 如果设置了此标志，NDISWAN 将通过未解释和未修改的帧。

微型端口驱动程序必须处于默认的 PPP 组帧模式，直到每个小型端口驱动程序都收到 [OID \_ WAN \_ CO \_ 集 \_ 链接 \_ 信息](oid-wan-co-set-link-info.md) 请求。 微型端口驱动程序必须自动检测它声明支持的任何帧。

例如，支持旧 RAS 帧的微型端口驱动程序必须自动检测 PPP 帧中的 RAS 帧。 如果微型端口驱动程序检测到默认情况以外的组帧方案，则该微型端口驱动程序应自动将其帧切换到新检测到的帧中。

带有 [OID \_ WAN \_ CO \_ 获取 \_ 链接 \_ 信息](oid-wan-co-get-link-info.md) 的后续查询应指示检测到的帧。 如果尚未检测到帧，则返回 **FramingBits** 的 NDIS \_ WAN \_ CO \_ 获取 \_ 链接 \_ 信息信息中的 FramingBits 应为零。

如果随后在 \_ \_ FramingBits 成员为零的 OID wan CO 集链接信息中调用 WAN 微型端口驱动程序 \_ \_ \_ ，则微型端口驱动程序应尝试在每个帧接收时自动检测组帧。 **FramingBits**

<a href="" id="desiredaccm"></a>**DesiredACCM**  
对异步控制字符映射进行协商。 此成员仅适用于异步媒体类型。

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


[**NdisMCoIndicateStatus**](/previous-versions/windows/hardware/network/ff553458(v=vs.85))

[OID \_ WAN \_ CO \_ 获取 \_ 链接 \_ 信息](oid-wan-co-get-link-info.md)

[OID \_ WAN \_ CO \_ 集 \_ 链接 \_ 信息](oid-wan-co-set-link-info.md)

[**WAN \_ CO \_ LINKPARAMS**](/previous-versions/windows/hardware/network/ff565819(v=vs.85))
