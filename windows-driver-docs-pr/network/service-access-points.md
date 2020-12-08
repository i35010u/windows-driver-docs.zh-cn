---
title: 服务接入点
description: 服务接入点
keywords:
- 传入呼叫 WDK CoNDIS
- 面向连接的 NDIS WDK，服务访问点
- CoNDIS WDK 网络，服务接入点
- 服务访问点 WDK CoNDIS
- Sap WDK CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 496d4a7cb5ca3b17e75771ec0049567376f35664
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812815"
---
# <a name="service-access-points"></a>服务接入点





*服务访问点* (SAP) 标识面向连接的客户端的相关传入调用的特征。 通过向呼叫管理器或 MCM 驱动程序注册 SAP，客户端会指示调用管理器或 MCM 驱动程序应通知客户端发送到该 SAP 的所有传入呼叫。

例如，如果客户端不处理传入的调用，则不会始终注册 SAP。 客户端可以向呼叫管理器或 MCM 驱动程序注册多个 Sap。

有关 Sap 的详细信息，请参阅 [注册 sap](registering-a-sap.md) 和 [注销 sap](deregistering-a-sap.md)。

 

 





