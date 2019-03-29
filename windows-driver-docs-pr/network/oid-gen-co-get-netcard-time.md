---
title: OID_GEN_CO_GET_NETCARD_TIME
description: 本主题介绍 OID_GEN_CO_GET_NETCARD_TIME 对象标识符 (OID)。
ms.assetid: 4dfa0f02-2b37-4b9f-95fe-dd33774dedbc
keywords:
- OID_GEN_CO_GET_NETCARD_TIME
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd55b2703f6b691084f8928de0dcd8ec6e564f6f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568610"
---
# <a name="oidgencogetnetcardtime"></a>OID_GEN_CO_GET_NETCARD_TIME

> [!NOTE]
> OID_GEN_CO_GET_NETCARD_TIME 是 OID_GEN_GET_NETCARD_TIME 相同。

OID_GEN_CO_GET_NETCARD_TIME OID 请求微型端口驱动程序，以返回 NIC 的本地时间，作为派生的 NIC 上一个时钟或网络。 时间格式为 GEN_GET_NETCARD_TIME 定义的结构，按如下所示：

```c++
typedef struct _GEN_GET_NETCARD_TIME{
    ULONGLONG   ReadTime;
} GEN_GET_NETCARD_TIME, *PGEN_GET_NETCARD_TIME;
```

此结构的成员包含以下信息：

**ReadTime**  
    NIC 的本地时间。

## <a name="remarks"></a>备注

微型端口驱动程序指定在其本地时间的单位**ClockPrecision**微型端口驱动程序返回到上一个 OID_GEN_CO_GET_TIME_CAPS 查询响应中 GEN_GET_TIME_CAPS 结构的元素。

如果微型端口驱动程序在其发送给 OID_GEN_CO_GET_TIME_CAPS 查询响应中设置 READABLE_LOCAL_CLOCK 标志，NIC 将其本地时间派生载入时钟。 如果微型端口驱动程序在其发送给 OID_GEN_CO_GET_TIME_CAPS 查询响应中设置 CLOCK_NETWORK_DERIVED 标志，NIC 从网络中派生其本地时间。

如果本地时间派生自登记的时钟，微型端口驱动程序应能够报告每个部分中的时钟精度 100 万条。 一般情况下，网络派生时钟是更可取，因为它可能更准确地说，可以用于同步多个计算机连接到同一网络或开关。

微型端口驱动程序必须返回其本地时间以同步方式 OID_GEN_CO_GET_NETCARD_TIME 查询其响应由于此查询与 NIC 的本地时间同步协议驱动程序。 协议驱动程序应发送 OID_GEN_CO_GET_NETCARD_TIME 查询几次连续筛选出响应时间的延迟。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 版本 | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

