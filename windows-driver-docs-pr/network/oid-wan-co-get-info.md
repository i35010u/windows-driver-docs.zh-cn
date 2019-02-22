---
title: OID_WAN_CO_GET_INFO
description: OID_WAN_CO_GET_INFO OID 请求微型端口驱动程序，以返回应用于其 NIC 上的所有虚拟连接 (VCs) 的信息 按如下所示定义 NDIS_WAN_CO_INFO 结构中返回此信息。
ms.assetid: c97130a5-68e1-4c69-a5a5-9781ea59af0c
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WAN_CO_GET_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 29e5b4f9b6f884c20df931c7f9b15964047ec358
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525307"
---
# <a name="oidwancogetinfo"></a>OID\_WAN\_共同\_获取\_信息


OID\_WAN\_共同\_获取\_信息 OID 请求微型端口驱动程序，以返回应用于其 NIC 上的所有虚拟连接 (VCs) 的信息 此信息返回在 NDIS\_WAN\_共同\_定义，如下所示的信息结构。

```ManagedCPlusPlus
    typedef struct _NDIS_WAN_CO_INFO {
         OUT ULONG MaxFrameSize;
         OUT ULONG MaxSendWindow;
         OUT ULONG FramingBits;
         OUT ULONG DesiredACCM;
    } NDIS_WAN_CO_INFO, *PNDIS_WAN_CO_INFO;
```




此结构的成员包含下列信息：

<a href="" id="maxframesize"></a>**MaxFrameSize**  
指定任何网络数据包的微型端口驱动程序可以发送和接收的最大帧大小。 此值应排除微型端口驱动程序自己的分帧开销和/或 PPP HDLC 开销。 通常，此值为约 1500年。

但是，所有的 CoNDIS WAN 的微型端口驱动程序应使用内部**MaxFrameSize** ，它是 32 个字节超出此 OID 它们返回的值。 例如，返回此 OID 1500 CoNDIS WAN 微型端口驱动程序在内部会接受并发送最多 1532年。 将来的桥接和其他协议，可以轻松地支持这样的微型端口驱动程序。

<a href="" id="maxsendwindow"></a>**MaxSendWindow**  
VC 上指定的最大未完成的 CoNDIS WAN 微型端口驱动程序可以处理的数据包数。 此成员必须设置为至少一个。

NDISWAN 驱动程序使用此成员的值作为其提交中的数据包数量将请求发送到微型端口驱动程序的限制*MiniportCoSendPackets*函数之前 NDISWAN 保留发送的数据包。 这些数据包进行排队，直到微型端口驱动程序完成未完成发送。 微型端口驱动程序可以调整此值，动态和 VC 每个使用**SendWindow**中的成员[ **WAN\_CO\_LINKPARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff565819)结构的微型端口驱动程序将传递给[ **NdisMCoIndicateStatus**](https://msdn.microsoft.com/library/windows/hardware/ff553458)。 NDISWAN 使用当前**SendWindow**与未完成发送其上限的值。 如果微型端口驱动程序设置**SendWindow** NDISWAN 必须为零，停止将数据包发送有关特定 VC。 也就是说，微型端口驱动程序指定发送窗口为实际上关闭的情况下，其中，，指定其无法接受来自 NDISWAN 任何数据包。

因为 CoNDIS WAN 的微型端口驱动程序必须在内部，队列数据包的值**MaxSendWindow**理论上是**max**(ULONG)。 但是，此驱动程序确定该值应反映 NIC 的链接速度或硬件功能 例如，如果微型端口驱动程序的 NIC 始终具有至少四个数据包的空间，微型端口驱动程序集**MaxSendWindow**至 4，以便为任何传入数据包*MiniportCoSendPackets*可以放置在立即在硬件中。

<a href="" id="framingbits"></a>**FramingBits**  
一个 32 位值，该值指定指定的分帧微型端口驱动程序支持的类型的位掩码。 微型端口驱动程序可以指定以下值，使用二进制或运算符的组合：

<a href="" id="ras-framing"></a>RAS\_FRAMING  
仅当微型端口驱动程序可以检测到较旧的 RAS 组帧设置。 仅旧版的驱动程序支持早期 RAS 组帧设置此标志。

<a href="" id="ras-compression"></a>RAS\_压缩  
仅当微型端口驱动程序支持的较旧的 RAS 压缩方案设置。

<a href="" id="ppp-framing"></a>PPP\_组帧  
应始终设置。 指示微型端口驱动程序可以检测并对其介质类型的支持 PPP 帧。

<a href="" id="ppp-compress-address-control"></a>PPP\_压缩\_地址\_控件  
如果微型端口驱动程序支持 PPP 地址和控件字段压缩，设置。

如果此 LCP 选项进行协商，NDISWAN 将删除的地址和控件的字段。 某些 WAN 的介质类型，如 X.25，不支持此选项。

<a href="" id="ppp-compress-protocol-field"></a>PPP\_压缩\_协议\_字段  
如果微型端口驱动程序支持 PPP 协议字段压缩，设置。

NDISWAN 将从协议字段时此 LCP 选项进行协商，适用于删除 1 个字节。

<a href="" id="ppp-accm-supported"></a>PPP\_ACCM\_支持  
如果该微型端口驱动程序支持异步控件字符映射，设置。 此位才有效的异步媒体，如调制解调器。 如果设置此位**DesiredACCM**成员都应有效。

<a href="" id="ppp-multilink-framing"></a>PPP\_多链路\_组帧  
如果微型端口驱动程序支持多个链接组帧 IETF RFC 1717 中指定，设置。

<a href="" id="ppp-short-sequence-hdr-format"></a>PPP\_短\_序列\_HDR\_格式  
如果微型端口驱动程序支持多个链接组帧 IETF RFC 1717 中指定的标头格式，设置。

<a href="" id="slip-framing"></a>SLIP\_组帧  
如果微型端口驱动程序可检测到并支持单组帧 （仅限异步微型端口驱动程序），设置。

<a href="" id="slip-vj-compression"></a>SLIP\_VJ\_压缩  
如果微型端口驱动程序可以支持单 Van Jacobsen TCP/IP 标头压缩，设置。 NDISWAN 支持滑动\_VJ\_压缩 （使用 16 个插槽）。 异步支持单分帧的媒体 （串行微型端口驱动程序） 应设置此位。

异步媒体不需要编写任何代码，以支持 VJ 标头压缩。 它将负责 NDISWAN。

<a href="" id="slip-vj-autodetect"></a>SLIP\_VJ\_AUTODETECT  
如果微型端口驱动程序可以自动检测对名单 Van Jacobsen TCP/IP 标头压缩，设置。 NDISWAN 将自动检测 VJ 标头压缩。 如果它们支持单组帧异步媒体 （串行微型端口驱动程序） 应设置此位。

<a href="" id="tapi-provider"></a>TAPI\_提供程序  
如果该微型端口驱动程序支持 TAPI 服务提供程序 Oid，设置。 设置此位，除非 TAPI OID 调用不会给微型端口驱动程序。

<a href="" id="media-nrz-encoding"></a>媒体\_NRZ\_编码  
如果该微型端口驱动程序支持 NRZ 编码，例如 ISDN 某些媒体类型的 PPP 默认，设置。 此值保留供将来使用。

<a href="" id="media-nrzi-encoding"></a>媒体\_NRZI\_编码  
如果微型端口驱动程序支持 NRZI 编码，设置。 此值保留供将来使用。

<a href="" id="media-nlpid"></a>MEDIA\_NLPID  
如果具有微型端口驱动程序，并且可以在其帧中设置 NLPID，设置。 此值保留供将来使用。

<a href="" id="rfc-1356-framing"></a>RFC\_1356\_FRAMING  
如果微型端口驱动程序支持 IETF RFC 1356 X.25 和 ISDN 组帧，设置。 此值保留供将来使用。

<a href="" id="rfc-1483-framing"></a>RFC\_1483\_FRAMING  
如果该微型端口驱动程序支持 IETF RFC 1483 ATM 适配层 5 封装，设置。 此值保留供将来使用。

<a href="" id="rfc-1490-framing"></a>RFC\_1490\_FRAMING  
如果该微型端口驱动程序支持 IETF RFC 1490 帧中继组帧，设置。 此值保留供将来使用。

<a href="" id="nbf-preserve-mac-address"></a>NBF\_PRESERVE\_MAC\_ADDRESS  
设置如果微型端口驱动程序支持 IETF 组帧草稿中指定"PPP NETBIOS 帧控制协议 (NBFCP)。"

<a href="" id="shiva-framing"></a>SHIVA\_FRAMING  
由 NBF 取代\_保留\_MAC\_地址。

<a href="" id="pass-through-mode"></a>传递\_THROUGH\_模式  
如果微型端口驱动程序执行其自己的分帧，设置。 如果设置此标志，NDISWAN 传递未解释的和未修改的帧。

微型端口驱动程序必须在默认 PPP 帧模式，直到每个微型端口驱动程序收到[OID\_WAN\_共同\_设置\_链接\_信息](oid-wan-co-set-link-info.md)请求。 微型端口驱动程序必须自动检测其声明，以便支持任何帧。

例如，支持旧 RAS 分帧的微型端口驱动程序必须自动检测来自 PPP 帧的 RAS 框架设计。 如果微型端口驱动程序检测到非默认的组帧方案，该微型端口驱动程序应自动切换到新检测到的帧其组帧。

具有的后续查询[OID\_WAN\_共同\_获取\_链接\_信息](oid-wan-co-get-link-info.md)应指示检测到的帧。 如果尚未检测到任何帧， **FramingBits**应为零中返回的 NDIS\_WAN\_共同\_获取\_链接\_信息的信息。

如果使用 OID 随后调用 WAN 微型端口驱动程序\_WAN\_共同\_设置\_链接\_中的信息**FramingBits**成员为零，微型端口驱动程序应尝试自动检测时接收的每个帧的帧。

<a href="" id="desiredaccm"></a>**DesiredACCM**  
异步控件字符映射表进行协商。 此成员是仅适用于异步媒体类型。

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
<td><p>支持 Windows Vista 中的 NDIS 6.0 和 NDIS 5.1 驱动程序。 支持 NDIS 5.1 在 Windows XP 中的驱动程序。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NdisMCoIndicateStatus**](https://msdn.microsoft.com/library/windows/hardware/ff553458)

[OID\_WAN\_CO\_GET\_LINK\_INFO](oid-wan-co-get-link-info.md)

[OID\_WAN\_CO\_SET\_LINK\_INFO](oid-wan-co-set-link-info.md)

[**WAN\_CO\_LINKPARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff565819)








