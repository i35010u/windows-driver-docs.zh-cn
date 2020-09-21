---
title: 针对地址系列和 SAP 的操作
description: 针对地址系列和 SAP 的操作
ms.assetid: 0fc821bb-49a2-4631-8735-ef5217073ba9
keywords:
- 面向连接的 NDIS WDK，地址系列
- CoNDIS WDK 网络，地址系列
- 面向连接的 NDIS WDK，服务访问点
- CoNDIS WDK 网络，服务接入点
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 944a9760e7cdd3ae4ab43b4bf636b3adbbd9c719
ms.sourcegitcommit: 366a15d68eb58d01a8ca6de7b982f62ac8b7deaf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2020
ms.locfileid: "90812020"
---
# <a name="operations-on-address-families-and-saps"></a>针对地址系列和 SAP 的操作





呼叫管理器或 MCM 驱动程序必须将其呼叫管理器入口点注册到 NDIS，并将其调用管理器服务播发到面向连接的客户端。 有关向 NDIS 注册入口点的详细信息，请参阅 [CoNDIS Registration](condis-miniport-driver-registration.md)。

若要使用呼叫管理器或 MCM 驱动程序的调用管理器服务，面向连接的客户端必须使用该呼叫管理器或 MCM 驱动程序打开一个地址族。 若要接收传入呼叫，客户端还必须将一个或多个 Sap 注册到呼叫管理器或 MCM 驱动程序。

以下面向连接的操作涉及到满足系列和 Sap 的需要：

[注册和打开地址系列](registering-and-opening-an-address-family.md)

[注册 SAP](registering-a-sap.md)

[取消注册 SAP](deregistering-a-sap.md)

[关闭地址系列](closing-an-address-family.md)

 

 





