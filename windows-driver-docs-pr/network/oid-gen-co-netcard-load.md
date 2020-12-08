---
title: OID_GEN_CO_NETCARD_LOAD
description: 本主题介绍) OID_GEN_CO_NETCARD_LOAD 对象标识符 (OID。
keywords:
- OID_GEN_CO_NETCARD_LOAD
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a834c33bac22e4bbd309ccb7a7441b3b5d49430
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836767"
---
# <a name="oid_gen_co_netcard_load"></a>OID_GEN_CO_NETCARD_LOAD

> [!NOTE]
> OID_GEN_CO_NETCARD_LOAD 与 OID_GEN_NETCARD_LOAD 相同。

OID_GEN_CO_NETCARD_LOAD OID 返回面向连接的微型端口驱动程序的传输系统上的相对负载。 微型端口驱动程序通过计算从协议传输的数据量与实际发送的数据量（由返回到带有 [NdisMCoSendComplete](/previous-versions/windows/hardware/network/ff553475(v=vs.85))的协议的数据包所指示）之间的差异，来派生此数字。 结果是在任何时候，微型端口驱动程序中的未处理传输数据量。

由于这种统计信息的变化非常高，因此微型端口驱动程序端口应对其进行筛选。 最简单的筛选方法是保持未完成传输数据的采样的运行平均值。 例如，每次调用 [MiniportCoSendPackets](/previous-versions/windows/hardware/network/ff549426(v=vs.85)) 时，微型端口驱动程序都可以将提交的数据包大小添加到名为 *OutstandingBytes* 的小型小型驱动程序定义的变量中。 每次微型小型驱动程序调用 [NdisMCoSendComplete](/previous-versions/windows/hardware/network/ff553475(v=vs.85))时，微型端口驱动程序将从 *OutstandingBytes* 中减去返回的数据包大小。 微型端口驱动程序还必须保持运行平均值，这是小型端口驱动程序为响应 OID_GEN_CO_NETCARD_LOAD 查询而返回的值。 此变量可称为 *RunningAverage*，必须在每个 *MiniportCoSendPackets* 上更新，如下所示：

```c++
RunningAverage = [(RunningAverage * C) + (OutstandingBytes * (128 - C))] / 128;
```
在这种情况下，为 1 \< *C* \< 128。 *C* 的值越大，筛选速度越平滑。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 
