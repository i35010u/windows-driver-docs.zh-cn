---
title: 查询面向连接的微型端口驱动程序
description: 查询面向连接的微型端口驱动程序
ms.assetid: 9e9926f6-cf90-48af-885f-59725721948d
keywords:
- 面向连接的驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b4de30e3ab57303a48b608173335fa4931e8c71
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349435"
---
# <a name="querying-a-connection-oriented-miniport-driver"></a>查询面向连接的微型端口驱动程序





若要查询的面向连接的微型端口驱动程序维护的信息对象，绑定的协议调用[ **NdisCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561711) ，并将传递[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构，它指定的对象 (OID) 正在查询中，并提供到 NDIS 最终写入所需的信息的缓冲区。 在调用**NdisCoOidRequest**会导致调用微型端口驱动程序的 NDIS [ *MiniportCoOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559362)函数，返回到 NDIS 所需的信息。 *MiniportCoOidRequest*可以通过调用完成同步或异步[ **NdisCoOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff561716)。

NDIS 还可以调用微型端口驱动程序[ *MiniportCoOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559362)代表其自身的函数-例如，在微型端口驱动程序[ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数已返回 NDIS\_状态\_成功 — 若要查询微型端口驱动程序的功能、 状态或统计信息。 下图说明了查询的面向连接的微型端口驱动程序。

![说明查询面向连接的微型端口驱动程序的关系图](images/fig5-3.png)

面向连接的微型端口驱动程序必须能够提供有关在全局基础信息的特定 NIC 的以及在每个 VC 的基础上的所有虚拟连接 (VCs)。 例如，如果一个非**NULL** *NdisVcHandle*提供给[ *MiniportCoOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559362)的查询[OID\_GEN\_CO\_RCV\_CRC\_错误](https://msdn.microsoft.com/library/windows/hardware/ff569562)，微型端口驱动程序返回的所有中遇到的 CRC 错误数接收指定 VC 上。 使用相同的请求**NULL** *NdisVcHandle*，微型端口驱动程序返回的所有传入都接收通过 NIC 遇到的 CRC 错误总数

以下列表包含的一套面向连接的微型端口驱动程序的必需常规操作 Oid:

[OID\_GEN\_共同\_支持\_列表](https://msdn.microsoft.com/library/windows/hardware/ff569567)

[OID\_GEN\_CO\_HARDWARE\_STATUS](https://msdn.microsoft.com/library/windows/hardware/ff569452)

[OID\_GEN\_共同\_媒体\_支持](https://msdn.microsoft.com/library/windows/hardware/ff569558)

[OID\_GEN\_CO\_MEDIA\_IN\_USE](https://msdn.microsoft.com/library/windows/hardware/ff569557)

[OID\_GEN\_CO\_LINK\_SPEED](https://msdn.microsoft.com/library/windows/hardware/ff569453)

[OID\_GEN\_CO\_VENDOR\_ID](https://msdn.microsoft.com/library/windows/hardware/ff569571)

[OID\_GEN\_共同\_供应商\_说明](https://msdn.microsoft.com/library/windows/hardware/ff569569)

[OID\_GEN\_CO\_VENDOR\_DRIVER\_VERSION](https://msdn.microsoft.com/library/windows/hardware/ff569570)

[OID\_GEN\_CO\_DRIVER\_VERSION](https://msdn.microsoft.com/library/windows/hardware/ff569449)

[OID\_GEN\_共同\_MAC\_选项](https://msdn.microsoft.com/library/windows/hardware/ff569454)

[OID\_GEN\_共同\_媒体\_CONNECT\_状态](https://msdn.microsoft.com/library/windows/hardware/ff569455)

[OID\_GEN\_共同\_最小值\_链接\_速度](https://msdn.microsoft.com/library/windows/hardware/ff569559)

微型端口驱动程序[ *MiniportCoOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559362)函数必须准备好响应查询或设置，根据需要，向任何前面的 Oid。

当[ *MiniportCoOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559362)调用使用 OID\_常规\_共同\_MAC\_选项，它必须返回指定可选的位掩码微型端口驱动程序执行的操作。 将该组标志包括：

-   NDIS\_MAC\_选项\_否\_环回。 如果设置此标志，微型端口驱动程序不传递到的数据包会不环回[ **MiniportCoSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff559365)定向到在同一台计算机上接收方的微型端口驱动程序需要 NDIS 执行环回。 如果 NDIS 执行数据包的环回，数据包不传递给微型端口驱动程序。 除非 NIC 执行硬件环回，微型端口驱动程序始终会设置此标志。

-   NDIS\_MAC\_ETOX\_指示。 如果设置此标志，微型端口驱动程序将指示发送已完成，只有在 NIC 将数据包发送后。

微型端口驱动程序必须永远不会使用 NDIS\_MAC\_选项\_保留的标志，保留供 NDIS 内部使用。

[*MiniportCoOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559362)还将使用特定于媒体的 OID，若要确定 NIC 的当前地址进行查询。

有关详细信息，请参阅[Connection-Oriented 调用管理器和客户端的 Oid](https://msdn.microsoft.com/library/windows/hardware/ff569067)并[常规对象](https://msdn.microsoft.com/library/windows/hardware/ff546510)。

 

 





