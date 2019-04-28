---
title: 接收远程 NDIS QoS 参数
description: 接收远程 NDIS QoS 参数
ms.assetid: 775FA8D7-ECF7-4F94-8958-C51D74243C3A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 280c19391778b6f92a354fcbca65e8d00c6b6c09
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349427"
---
# <a name="receiving-remote-ndis-qos-parameters"></a>接收远程 NDIS QoS 参数


远程 NDIS 服务质量 (QoS) 参数是指那些来自通过数据链接的网络适配器连接到远程对等方。 微型端口驱动程序将发现这些参数通过 IEEE 802.1Qaz 由指定的数据中心桥接交换 (DCBX) 协议草案标准。

该驱动程序必须遵循这些准则以管理远程 QoS 参数：

-   微型端口驱动程序必须发出[ **NDIS\_状态\_QOS\_远程\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439812)状态指示时其远程 NDIS QoS 参数既接收来自对等方第一次或更高版本更改。 此过程的详细信息，请参阅[对远程 NDIS QoS 参数，该值指示更改](indicating-changes-to-the-remote-ndis-qos-parameters.md)。

-   微型端口驱动程序可以使用远程 NDIS QoS 参数以在网络适配器上启用了本地数据中心桥接交换 (DCBX) 愿意状态时才解析其操作的 NDIS QoS 参数。 微型端口驱动程序也可以解决基于由独立硬件供应商 (IHV) 定义的任何专有 QoS 设置其操作的 QoS 参数。

    有关此过程的详细信息，请参阅[解析操作的 NDIS QoS 参数](resolving-operational-ndis-qos-parameters.md)。

    有关本地 DCBX 愿意状态，请参阅[管理本地 DCBX 愿意状态](managing-the-local-dcbx-willing-state.md)。

NDIS QoS 参数的详细信息，请参阅[NDIS QoS 参数的概述](overview-of-ndis-qos-parameters.md)。

 

 





