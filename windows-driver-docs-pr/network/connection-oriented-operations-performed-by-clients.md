---
title: 客户端执行的面向连接的操作
description: 客户端执行的面向连接的操作
keywords:
- 面向连接的客户端 WDK
- 客户端操作 WDK CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d5c33fad54bfd448c1cae0bd78174f70968aed5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813717"
---
# <a name="connection-oriented-operations-performed-by-clients"></a>客户端执行的面向连接的操作





面向连接的客户端：

-   **打开并关闭地址族。**

    在从 NDIS 接收到呼叫管理器或 MCM 驱动程序已注册地址族的通知时，面向连接的驱动程序可以使用呼叫管理器或 MCM 驱动程序 [打开该地址系列](registering-and-opening-an-address-family.md) 。 然后，客户端可以使用呼叫管理器或 MCM 驱动程序提供的呼叫管理器服务。 客户端通过 [关闭地址族](closing-an-address-family.md)，释放自身与调用管理器或 MCM 驱动程序之间的关联。

-   **注册并注销 Sap。**

    使用呼叫管理器或 MCM 驱动程序打开地址族后，面向连接的客户端可以使用呼叫管理器或 MCM 驱动程序 [注册一个或多个 sap](registering-a-sap.md) 。 然后，调用管理器或 MCM 驱动程序向客户端指明发送到注册的 Sap 的任何传入呼叫。 客户端通过 [注销 sap](deregistering-a-sap.md)来释放 sap。

-   **添加和删除 Pvc。**

    面向连接的客户端可以在操作员手动配置或取消配置永久 VC (PVC) 时进行监视。 为响应此类操作，客户端可以请求调用管理器或 MCM 驱动程序将 PVC 添加到其已配置的 Pvc 列表，或从此类列表中删除 PVC (参阅 [OID \_ co \_ Add \_ pvc](./oid-co-add-pvc.md) and [oid \_ co \_ delete \_ pvc](./oid-co-delete-pvc.md)) 。

-   **发出传出呼叫。**

    发出传出呼叫之前，客户端必须启动为该调用 [创建 VC](creating-a-vc.md) 。 然后，客户端可以 [发出传出呼叫](making-a-call.md)。 若要进行点对多点调用，客户端在进行调用时指定参与方。

-   **在点到 multipoint 调用中添加或删除参与方。**

    客户端可以向 [点到 multipoint 呼叫添加参与](adding-a-party-to-a-multipoint-call.md) 方，并 [从点到 multipoint 调用中删除参与方](dropping-a-party-from-a-multipoint-call.md)。 客户端还可以响应 [从点到 multipoint 调用中删除参与方](incoming-request-to-drop-a-party-from-a-multipoint-call.md)的传入请求。

-   **接受或拒绝传入呼叫。**

    客户端可以 [接受或拒绝](indicating-an-incoming-call.md) 寻址到客户端以前使用调用管理器或 MCM 驱动程序注册的 SAP 的传入呼叫。

-   **协商活动 VC 的调用参数。**

    根据信号协议允许的内容，客户端可以协商活动 VC 的调用参数。 客户端 (QoS) 并响应传入请求以更改活动 VC 的 QoS，从而 [请求更改服务质量 ](client-initiated-request-to-change-call-parameters.md) 。 客户端还可以响应 [远程方的请求，以更改呼叫的 QoS](incoming-request-to-change-call-parameters.md)。

-   **发送和接收数据包。**

    客户端可以通过面向连接的微型端口驱动程序或 MCM 驱动程序来发送数据包。 客户端还可以通过面向连接的微型端口驱动程序或 MCM 驱动程序接收数据包。

-   **启动删除 VC。**

    客户端可以启动它创建 [的 VC 的删除](deleting-a-vc.md) 。

-   **启动调用的细分。**

    客户端可以对它发出的 [传出呼叫](client-initiated-request-to-close-a-call.md) 或它接受的传入呼叫启动分离。

-   **查询或设置信息。**

    客户端可以查询或设置由绑定调用管理器或 MCM 驱动程序的调用管理器部分维护的信息。 客户端还可以响应绑定调用管理器或 MCM 驱动程序的 [查询和集](querying-or-setting-information.md) 。

    此外，客户端可以查询或设置绑定的微型端口驱动程序或绑定 MCM 驱动程序的微型端口驱动程序部分所维护的信息。

-   **Inputsminiport 驱动程序状态指示。**

    客户端可以输入 [由面向连接的微型端口驱动程序](indicating-miniport-driver-status.md) 或 MCM 驱动程序指示的状态。

 

