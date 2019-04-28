---
title: 服务接入点
description: 服务接入点
ms.assetid: a6fab686-6adb-4d77-8f0d-2b48e2e49f1f
keywords:
- 传入呼叫 WDK 的 CoNDIS
- 面向连接的 NDIS WDK、 服务访问点
- CoNDIS WDK 网络、 服务访问点
- 服务访问点 WDK 的 CoNDIS
- SAPs WDK CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b23a35d0aa405d4ba2b413e76b854e8f9e60827c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346771"
---
# <a name="service-access-points"></a>服务接入点





一个*服务访问点*(SAP) 标识的感兴趣的面向连接的客户端的传入呼叫的特征。 通过注册 SAP 呼叫管理器或 MCM 驱动程序，客户端指示呼叫管理器或 MCM 驱动程序应通知发送到 SAP 的所有传入调用的客户端。

客户端不会始终注册 SAP 的例如，如果它无法处理传入的呼叫。 客户端可以注册多个 SAPs 呼叫管理器或 MCM 驱动程序。

有关 Sap 的详细信息，请参阅[注册 SAP](registering-a-sap.md)并[取消 SAP](deregistering-a-sap.md)。

 

 





