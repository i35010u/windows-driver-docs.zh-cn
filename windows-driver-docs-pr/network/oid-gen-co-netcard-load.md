---
title: OID_GEN_CO_NETCARD_LOAD
description: 本主题介绍 OID_GEN_CO_NETCARD_LOAD 对象标识符 (OID)。
ms.assetid: 0fdf9948-6b1a-48c9-87a4-7ecdfd1a8e47
keywords:
- OID_GEN_CO_NETCARD_LOAD
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01541c1829694c3ad8896755d121041bc6ece685
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348207"
---
# <a name="oidgenconetcardload"></a>OID_GEN_CO_NETCARD_LOAD

> [!NOTE]
> OID_GEN_CO_NETCARD_LOAD 是 OID_GEN_NETCARD_LOAD 相同。

OID_GEN_CO_NETCARD_LOAD OID 在面向连接的微型端口驱动程序的传输系统返回相对负载。 微型端口驱动程序通过返回到包含协议的数据包所示计算传送用于从协议传输的数据量和实际发送的数据量之间的差异来派生此数字[NdisMCoSendComplete](https://msdn.microsoft.com/library/windows/hardware/ff553475)。 结果是未处理的量在任何时候传输微型端口驱动程序中的数据。

由于此统计信息更改非常频繁，微型端口驱动程序端口应筛选器。 最简单的筛选方法是保持正在运行的未完成的样本的平均值传输数据。 例如，每次[MiniportCoSendPackets](https://msdn.microsoft.com/library/windows/hardware/ff549426)调用时，微型端口驱动程序无法将已提交的数据包大小添加到名为的微型端口驱动程序定义变量*OutstandingBytes*。 每次微型端口驱动程序调用[NdisMCoSendComplete](https://msdn.microsoft.com/library/windows/hardware/ff553475)，微型端口驱动程序将然后减去从返回的数据包大小*OutstandingBytes*。 微型端口驱动程序还必须始终是正在运行的平均值，即微型端口驱动程序应在 OID_GEN_CO_NETCARD_LOAD 查询响应中返回的值。 此变量，可以调用*RunningAverage*，必须更新每个*MiniportCoSendPackets*，按如下所示：

```c++
RunningAverage = [(RunningAverage * C) + (OutstandingBytes * (128 - C))] / 128;
```
在本例中为 1 \< *C* \< 128。 较大的值*C*生成更顺畅地筛选。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |