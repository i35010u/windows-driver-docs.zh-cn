---
title: OID_GEN_CO_GET_TIME_CAPS
description: 本主题介绍 OID_GEN_CO_GET_TIME_CAPS 对象标识符 (OID)。
ms.assetid: 6381cfc4-b070-4bd4-90de-6de8a4656cbb
keywords:
- OID_GEN_CO_GET_TIME_CAPS
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 574b33cce46ddbd0f1b745cc154c6901f9e819d1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379271"
---
# <a name="oidgencogettimecaps"></a>OID_GEN_CO_GET_TIME_CAPS

> [!NOTE]
> OID_GEN_CO_GET_TIME_CAPS 是 OID_GEN_GET_TIME_CAPS 相同。

OID_GEN_CO_GET_TIME_CAPS OID 请求微型端口驱动程序返回用于报告 NIC 的本地时间格式为 GEN_GET_TIME_CAPS 结构，按如下所示定义其功能：

```c++
typedef struct _GEN_GET_TIME_CAPS{
    ULONG   Flags;
    ULONG   ClockPrecision;
} GEN_GET_TIME_CAPS, *PGEN_GET_TIME_CAPS;
```

此结构的成员包含下列信息：

**标志**  
以下标志可以一起或运算。 所有未指定的标志必须设置为零。 

READABLE_LOCAL_CLOCK  
设置时，指示存在可读时钟上的 nic。 即使没有此类硬件时钟，微型端口驱动程序可以使用系统时钟通过调用 NdisGetCurrentSystemTime，只要它报告 ClockPrecision 成员中的正确精度。

CLOCK_NETWORK_DERIVED  
设置时，指示 NIC 的本地时间从网络连接，而不是免费运行载入时钟派生。

CLOCK_PRECISION  
设置时，指示 ClockPrecision 成员包含有效的信息。

RECEIVE_TIME_INDICATION_CAPABLE  
设置时，指示 NIC 硬件可以记下的接收已接收的 PDU 的第一个单元格和微型端口驱动程序将传播此时间为每个 PDU 时收到，该值指示为协议的数据包的本地时间。

TIMED_SEND_CAPABLE  
设置时，指示 NIC 可以计划按照其本地时间的传输的数据包。 协议可以使用 NDIS_SET_PACKET_TIME_TO_SEND 数据包描述符的带外数据块中设置 TimeToSend 时间戳。 设置时间戳不会影响时实际传输该数据包;相反，时间戳用于记录保留。 协议驱动程序可以使用时间戳来确定它所需的时间完成 paket 依存的发送。

TIME_STAMP_CAPABLE  
设置时，指示，NIC 可以标记 （在相应字段中的传出数据包） 的时间而该传输数据包的第一个字节和 NIC 可以检索从入站数据包的相同字段的这一次。

**ClockPrecision**  
在每个部分中指定的时钟精度 100 万条。 获取此信息才被视为有效，必须设置 CLOCK_PRECISION 标志。

## <a name="remarks"></a>备注

微型端口驱动程序可以提供某些甚至在没有本地或网络时钟计时参数的支持。 具体而言，微型端口驱动程序可以使用系统时钟的接收时间指示、 定时的发送和甚至时间戳。 基于 NIC 的时钟会更好的因为它是可能提供较高的精度，并且可以访问与系统时钟更低的延迟。 在所有情况下，微型端口驱动程序必须指定它使用时钟的精度。 这样，以确定如何最好地使用微型端口驱动程序的计时支持的协议。

如果微型端口驱动程序报告的可读的时钟存在，它必须准备好立即响应 OID_GEN_GET_NETCARD_TIME 查询。 此调用的微型端口驱动程序的响应是时间关键的因此必须同步。


## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

