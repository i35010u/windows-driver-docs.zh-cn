---
title: OID_GEN_CO_GET_TIME_CAPS
description: 本主题介绍) OID_GEN_CO_GET_TIME_CAPS 对象标识符 (OID。
keywords:
- OID_GEN_CO_GET_TIME_CAPS
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb7627bd5f554e9f6c1f11840f0cf012e82245af
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792653"
---
# <a name="oid_gen_co_get_time_caps"></a>OID_GEN_CO_GET_TIME_CAPS

> [!NOTE]
> OID_GEN_CO_GET_TIME_CAPS 与 OID_GEN_GET_TIME_CAPS 相同。

OID_GEN_CO_GET_TIME_CAPS OID 请求微型端口驱动程序返回其功能，以将 NIC 的本地时间报告为 GEN_GET_TIME_CAPS 结构，如下所示：

```c++
typedef struct _GEN_GET_TIME_CAPS{
    ULONG   Flags;
    ULONG   ClockPrecision;
} GEN_GET_TIME_CAPS, *PGEN_GET_TIME_CAPS;
```

此结构的成员包含以下信息：

**标记**  
以下标志可以运算在一起。 所有未指定的标志都必须设置为零。 

READABLE_LOCAL_CLOCK  
如果设置，则表示 NIC 上存在可读时钟。 即使没有这样的硬件时钟，微型端口驱动程序也可以通过调用 NdisGetCurrentSystemTime 来使用系统时钟，前提是它在 ClockPrecision 成员中报告了正确的精度。

CLOCK_NETWORK_DERIVED  
如果设置此项，则表示 NIC 的本地时间是从网络连接派生而来的，而不是一个免费运行的板载时钟。

CLOCK_PRECISION  
如果设置，则指示 ClockPrecision 成员包含有效的信息。

RECEIVE_TIME_INDICATION_CAPABLE  
如果设置，则表示 NIC 硬件可以记下接收到的 PDU 的第一个单元格的本地时间，而微型端口驱动程序会在指示数据包到协议时为每个 PDU 传播此接收时间。

TIMED_SEND_CAPABLE  
如果设置此设置，则表示 NIC 可以根据本地时间来计划要传输的数据包。 协议可以使用 NDIS_SET_PACKET_TIME_TO_SEND 设置数据包描述符的带外数据块中的 TimeToSend 时间戳。 设置时间戳不影响数据包的实际传输时间;相反，时间戳用于记录保留。 协议驱动程序可以使用时间戳来确定完成发送 paket 所用的时间。

TIME_STAMP_CAPABLE  
如果设置，则表示 NIC 可以在传出数据包的相应字段中标记 () 发送数据包的第一个字节的时间，NIC 可以从入站数据包的同一个字段中检索此时间。

**ClockPrecision**  
指定各部分中的时钟精度（以百万为单位）。 若要将此信息视为有效，必须设置 CLOCK_PRECISION 标志。

## <a name="remarks"></a>备注

小型小型驱动程序可以为某些计时参数提供支持，即使在缺少本地或网络时钟时也是如此。 特别是，小型端口驱动程序可以使用系统时钟进行接收时间指示、计时发送，甚至时间戳。 基于 NIC 的时钟更好，因为它可能会提供更高的精度，并且与系统时钟相比，延迟更低。 在所有情况下，微型端口驱动程序必须指定其使用的时钟的精度。 这允许协议确定如何最大程度地使用微型端口驱动程序的计时支持。

如果微型端口驱动程序报告可读时钟的状态，则必须准备好立即响应 OID_GEN_GET_NETCARD_TIME 查询。 小型端口驱动程序对此调用的响应是时间关键的，因此必须是同步的。


## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 

