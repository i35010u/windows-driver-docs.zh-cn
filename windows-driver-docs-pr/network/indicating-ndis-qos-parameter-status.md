---
title: 指示 NDIS QoS 参数状态
description: 指示 NDIS QoS 参数状态
ms.assetid: 7E896BC3-839F-4119-BF79-A7BB4CA61CDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78dec8376f7df295cfee5dac65ed75e13d30de87
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576845"
---
# <a name="indicating-ndis-qos-parameter-status"></a>指示 NDIS QoS 参数状态


IEEE 802.1 数据中心桥接 (DCB) 接口支持 NDIS 服务质量 (QoS) 的微型端口驱动程序必须发出 NDIS 状态指示，只要发生以下事件之一：

-   驱动程序的操作的 NDIS QoS 参数或者解决第一次或更高版本更改。

    有关如何颁发 NDIS 状态指示该类型的详细信息，请参阅[对操作的 NDIS QoS 参数，该值指示更改](indicating-changes-to-the-operational-ndis-qos-parameters.md)。

-   驱动程序的远程 NDIS QoS 参数或者从接收到数据链接对等方第一次或更高版本更改。

    有关如何颁发 NDIS 状态指示该类型的详细信息，请参阅[对远程 NDIS QoS 参数，该值指示更改](indicating-changes-to-the-remote-ndis-qos-parameters.md)。

有关操作和远程 NDIS QoS 参数的详细信息，请参阅[NDIS QoS 参数的概述](overview-of-ndis-qos-parameters.md)。

 

 





