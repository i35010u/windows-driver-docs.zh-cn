---
title: 地址系列和 SAPs 的操作
description: 地址系列和 SAPs 的操作
ms.assetid: 0fc821bb-49a2-4631-8735-ef5217073ba9
keywords:
- 面向连接的 NDIS WDK，地址系列
- CoNDIS WDK 网络、 地址系列
- 面向连接的 NDIS WDK、 服务访问点
- CoNDIS WDK 网络、 服务访问点
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97a4665814121328a6fdcf0ef9ef7e971944a316
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521772"
---
# <a name="operations-on-address-families-and-saps"></a>地址系列和 SAPs 的操作





呼叫管理器或 MCM 驱动程序必须使用 NDIS 注册其调用管理器入口点并播发到面向连接的客户端及其调用管理器服务。 使用 NDIS 注册 enttry 点的详细信息，请参阅[CoNDIS 注册](condis-registration.md)。

若要使用的呼叫管理器或 MCM 驱动程序的调用管理器服务，面向连接的客户端必须使用该呼叫管理器或 MCM 驱动程序打开地址族。 若要接收传入的呼叫，客户端还必须与呼叫管理器或 MCM 驱动程序中注册一个或多个 SAPs。

与地址系列和 SAPs 相关的以下面向连接的操作：

[注册并打开地址系列](registering-and-opening-an-address-family.md)

[注册 SAP](registering-a-sap.md)

[取消注册 SAP](deregistering-a-sap.md)

[关闭地址系列](closing-an-address-family.md)

 

 





