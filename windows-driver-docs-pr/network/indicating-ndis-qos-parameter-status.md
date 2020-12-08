---
title: 指示 NDIS QoS 参数状态
description: 指示 NDIS QoS 参数状态
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cacab0a0f4d0094ed7c34afe11a28901909b1c3c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837202"
---
# <a name="indicating-ndis-qos-parameter-status"></a>指示 NDIS QoS 参数状态


对于 IEEE 802.1 数据中心桥接 (DCB) 接口，支持 NDIS 服务 (QoS) 的微型端口驱动程序必须在发生以下任一事件时发出 NDIS 状态指示：

-   驱动程序的操作 NDIS QoS 参数是首次解决的，或者以后更改。

    有关如何发出此类型的 NDIS 状态指示的详细信息，请参阅 [指示对操作 Ndis QoS 参数的更改](indicating-changes-to-the-operational-ndis-qos-parameters.md)。

-   驱动程序的远程 NDIS QoS 参数是第一次从数据链路对等方接收的，或者以后更改。

    有关如何发出此类型的 NDIS 状态指示的详细信息，请参阅 [指示对远程 NDIS QoS 参数所做的更改](indicating-changes-to-the-remote-ndis-qos-parameters.md)。

有关操作和远程 NDIS QoS 参数的详细信息，请参阅 " [Ndis Qos 参数概述](overview-of-ndis-qos-parameters.md)"。

 

 





