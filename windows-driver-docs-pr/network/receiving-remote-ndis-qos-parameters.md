---
title: 接收远程 NDIS QoS 参数
description: 接收远程 NDIS QoS 参数
ms.assetid: 775FA8D7-ECF7-4F94-8958-C51D74243C3A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b49d2423a3fc605d46f74ca5e24f2cb87a4b57d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216934"
---
# <a name="receiving-remote-ndis-qos-parameters"></a>接收远程 NDIS QoS 参数


远程 NDIS 服务质量 (QoS) 参数是从网络适配器通过数据链路上的网络适配器连接到的远程对等机接收的参数。 微型端口驱动程序通过数据中心桥接 Exchange (DCBX) 由 IEEE 802.1 Qaz 草案标准指定的协议来发现这些参数。

驱动程序必须遵循以下准则来管理远程 QoS 参数：

-   小型端口驱动程序必须在第一次从对等方接收或更改其远程 NDIS QoS 参数时发出 [**NDIS \_ 状态 \_ QOS \_ 远程 \_ 参数 " \_ 更改**](./ndis-status-qos-remote-parameters-change.md) 状态指示"。 有关此过程的详细信息，请参阅 [指示对远程 NDIS QoS 参数所做的更改](indicating-changes-to-the-remote-ndis-qos-parameters.md)。

-   仅当本地数据中心桥接 Exchange (DCBX) 在网络适配器上启用了 "愿意" 状态时，微型端口驱动程序才可以使用远程 NDIS QoS 参数来解析其操作 NDIS QoS 参数。 微型端口驱动程序还可以根据独立硬件供应商 (IHV) 定义的任何专有 QoS 设置来解析其操作 QoS 参数。

    有关此过程的详细信息，请参阅 [解析操作 NDIS QoS 参数](resolving-operational-ndis-qos-parameters.md)。

    有关本地 DCBX 适用状态的详细信息，请参阅 [管理本地 DCBX 适用的状态](managing-the-local-dcbx-willing-state.md)。

有关 NDIS QoS 参数的详细信息，请参阅 " [Ndis Qos 参数概述](overview-of-ndis-qos-parameters.md)"。

 

