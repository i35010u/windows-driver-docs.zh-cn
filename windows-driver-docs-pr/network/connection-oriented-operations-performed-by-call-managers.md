---
title: 呼叫管理程序执行的面向连接的操作
description: 呼叫管理程序执行的面向连接的操作
ms.assetid: 6df23eb2-df02-4d24-88b3-c02b87edb38b
keywords:
- 面向连接的 NDIS WDK，呼叫管理器
- CoNDIS WDK 网络，呼叫管理器
- 呼叫经理 WDK 网络，面向连接的操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c39b9e9b15186bd2efa3f68458eccd90f28af84b
ms.sourcegitcommit: 366a15d68eb58d01a8ca6de7b982f62ac8b7deaf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2020
ms.locfileid: "90811920"
---
# <a name="connection-oriented-operations-performed-by-call-managers"></a>呼叫管理程序执行的面向连接的操作





调用管理器执行以下操作：

-   ** (AFs) 注册并注销一个或多个地址系列。**

    调用管理器使用 NDIS [注册一个或多个地址族](registering-and-opening-an-address-family.md) 。 通过注册地址族，呼叫管理器会公布其呼叫管理器服务 (具体而言，一种信号协议) 绑定到面向连接的客户端。 有关向 NDIS 注册入口点的信息，请参阅 [CoNDIS Registration](condis-miniport-driver-registration.md)。

-   **在面向连接的客户端的请求上注册并注销 Sap。**

    呼叫管理器接收绑定的面向连接的客户端的请求，以 [注册 sap](registering-a-sap.md) 并取消 [注册 sap](deregistering-a-sap.md)。 呼叫管理器通过网络发送信号消息，以代表客户端注册或取消注册 Sap。

-   **在面向连接的客户端请求时设置传出呼叫。**

    当面向连接的客户端 [发出传出呼叫](making-a-call.md)时，呼叫管理器会根据需要与网络控制设备) 的信号消息进行 (通信，以进行连接。 如果远程方接受调用，则调用管理器激活为该调用创建的 [VC](activating-a-vc.md) 。

-   **设置并指示对面向连接的客户端的传入调用。**

    呼叫管理器向绑定的面向连接的客户端指示所有寻址到该客户端注册的 SAP 的呼叫。 在 [指示传入](indicating-an-incoming-call.md) 客户端的调用之前，调用管理器开始为调用 [创建 vc](creating-a-vc.md) ，然后启动 [对 vc 的激活](activating-a-vc.md)。

-   **传达有关 QoS 中更改的请求。**

    根据信号协议，呼叫管理器可以与 [本地客户端的请求进行通信，以更改传出或传入呼叫的 qos](client-initiated-request-to-change-call-parameters.md) ，或 [来自远程方的请求以更改呼叫的 qos](incoming-request-to-change-call-parameters.md)。

-   **传递请求以添加和删除参与方。**

    呼叫管理器将本地客户端的请求与点到 multipoint 调用之间 [添加](adding-a-party-to-a-multipoint-call.md) 或 [删除参与](dropping-a-party-from-a-multipoint-call.md) 方通信。 呼叫管理器还会传达远程方的 [传入请求，以从点到 multipoint 调用中删除自身](incoming-request-to-drop-a-party-from-a-multipoint-call.md)。

-   **泪水调用。**

    在面向连接的客户端发出请求时，呼叫管理器通过与网络控制设备通信来 [终止连接](client-initiated-request-to-close-a-call.md)。 在远程方的请求中，呼叫管理器向本地面向连接的客户端指示远程方 [请求关闭呼叫](incoming-request-to-close-a-call.md)。 在撕裂调用的过程中，呼叫管理器会停用用于调用的 [VC](deactivating-a-vc.md) 。 如果调用管理器为传入调用) 创建了 VC (，则调用管理器也可以 [删除 vc](deleting-a-vc.md)。

-   **查询或设置信息。**

    呼叫管理器可以 [查询或设置](querying-or-setting-information.md) 由面向连接的连接的客户端所维护的信息。 调用管理器还可以响应基于连接的绑定客户端的查询和设置操作。

    此外，呼叫管理器还可以查询或设置由绑定的微型端口驱动程序或绑定 MCM 驱动程序的微型端口驱动程序部分维护的信息。

-   **Inputsminiport 驱动程序状态指示。**

    呼叫管理器会 [从面向连接的连接端口驱动程序中输入状态指示](indicating-miniport-driver-status.md)。

 

 





