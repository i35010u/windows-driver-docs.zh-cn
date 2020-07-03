---
title: OID_GEN_CO_GET_NETCARD_TIME
description: 本主题介绍 OID_GEN_CO_GET_NETCARD_TIME 对象标识符（OID）。
ms.assetid: 4dfa0f02-2b37-4b9f-95fe-dd33774dedbc
keywords:
- OID_GEN_CO_GET_NETCARD_TIME
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 944ba507a1b12bdad15c5d55676d9f8fbdead1ab
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916619"
---
# <a name="oid_gen_co_get_netcard_time"></a>OID_GEN_CO_GET_NETCARD_TIME

> [!NOTE]
> OID_GEN_CO_GET_NETCARD_TIME 与 OID_GEN_GET_NETCARD_TIME 相同。

OID_GEN_CO_GET_NETCARD_TIME OID 请求微型端口驱动程序返回 NIC 的本地时间，该时间是从 NIC 上的时钟或从网络中派生的。 此时间的格式为 GEN_GET_NETCARD_TIME 结构，定义如下：

```c++
typedef struct _GEN_GET_NETCARD_TIME{
    ULONGLONG   ReadTime;
} GEN_GET_NETCARD_TIME, *PGEN_GET_NETCARD_TIME;
```

此结构的成员包含以下信息：

**ReadTime**  
    NIC 的本地时间。

## <a name="remarks"></a>备注

微型端口驱动程序在 GEN_GET_TIME_CAPS 结构的**ClockPrecision**元素中指定了其本地时间单位，这是小型端口驱动程序为响应先前 OID_GEN_CO_GET_TIME_CAPS 查询而返回的。

如果微型端口驱动程序将 READABLE_LOCAL_CLOCK 标志设置为对 OID_GEN_CO_GET_TIME_CAPS 查询的响应，则 NIC 将从板载时钟中派生出其本地时间。 如果微型端口驱动程序将 CLOCK_NETWORK_DERIVED 标志设置为对 OID_GEN_CO_GET_TIME_CAPS 查询的响应，则 NIC 会从网络中派生出其本地时间。

如果本地时间是从板载时钟派生的，微型端口驱动程序应能够以百万为单位报告时钟精度。 通常，网络派生时钟更好，因为它可能更为精确，并且可用于同步连接到同一网络或交换机的多个计算机。

微型端口驱动程序必须在其对 OID_GEN_CO_GET_NETCARD_TIME 查询的响应中同步返回其本地时间，因为此查询会将协议驱动程序与 NIC 的本地时间同步。 协议驱动程序应连续多次发送 OID_GEN_CO_GET_NETCARD_TIME 查询，以筛选出响应时间延迟。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的**标头**： Ntddndis （包括 Ndis .h）

