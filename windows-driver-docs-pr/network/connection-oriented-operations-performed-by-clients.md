---
title: 客户端执行的面向连接的操作
description: 客户端执行的面向连接的操作
ms.assetid: 342f534e-d203-4823-a4d8-a8a51b7ff0bd
keywords:
- 面向连接的客户端 WDK
- 客户端操作 WDK 的 CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51f6d6b0820d31deb0a1ef0594c96634e90428f8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374957"
---
# <a name="connection-oriented-operations-performed-by-clients"></a>客户端执行的面向连接的操作





面向连接的客户端：

-   **打开和关闭的地址族。**

    在接收到通知从 NDIS 呼叫管理器或 MCM 驱动程序已注册的地址族，面向连接的驱动程序可以[打开该地址族](registering-and-opening-an-address-family.md)呼叫管理器或 MCM 驱动程序。 客户端然后可以使用提供的呼叫管理器或 MCM 驱动程序的调用管理器服务。 客户端发布本身与呼叫管理器或 MCM 驱动程序之间的关联[关闭的地址族](closing-an-address-family.md)。

-   **进行注册和注销 SAPs。**

    打开后的地址族与呼叫管理器或 MCM 驱动程序，面向连接的客户端可以[注册一个或多个 SAPs](registering-a-sap.md)呼叫管理器或 MCM 驱动程序。 呼叫管理器或 MCM 驱动程序将然后指示向客户端发送到已注册的 SAPs 的任何传入调用。 客户端版本的 SAP[取消注册 SAP](deregistering-a-sap.md)。

-   **添加和删除 Pvc。**

    操作员手动配置或可永久 VC (PVC) 时，可以监视面向连接的客户端。 在此操作的响应，客户端可以请求将 PVC 添加到配置 Pvc 其列表，或从这类列表中删除 PVC 的呼叫管理器或 MCM 驱动程序 (请参阅[OID\_共同\_添加\_PVC](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-add-pvc)并[OID\_CO\_删除\_PVC](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-delete-pvc))。

-   **使传出调用。**

    传出调用前，客户端必须启动[VC 创建](creating-a-vc.md)调用。 然后可以通过客户端[发起传出呼叫](making-a-call.md)。 若要使多点到点调用，客户端指定参与方时进行调用。

-   **添加到参与方或从多点到点调用删除参与方。**

    客户端可以[添加到多点到点调用的参与方](adding-a-party-to-a-multipoint-call.md)并[点 multipoint 调用删除参与方](dropping-a-party-from-a-multipoint-call.md)。 客户端还可以响应传入[请求以停止点 multipoint 调用方](incoming-request-to-drop-a-party-from-a-multipoint-call.md)。

-   **接受或拒绝的传入呼叫。**

    客户端可以[接受或拒绝的传入呼叫](indicating-an-incoming-call.md)，将发送给 SAP 客户端之前注册的呼叫管理器或 MCM 驱动程序。

-   **有关 active VC 协商调用参数。**

    具体取决于所允许的信号协议，客户端可以协商 active VC 调用参数。 客户端可以[请求的服务质量 (QoS) 中更改](client-initiated-request-to-change-call-parameters.md)并对要更改活动 VC QoS 的传入请求作出响应。 客户端还可以响应[从远程方的请求以更改调用 QoS](incoming-request-to-change-call-parameters.md)。

-   **发送和接收数据包。**

    客户端可以发送数据包通过面向连接的微型端口驱动程序或 MCM 驱动程序。 客户端还可以接收通过面向连接的微型端口驱动程序或 MCM 驱动程序的数据包。

-   **启动删除的 VC。**

    客户端可以启动[VC 删除](deleting-a-vc.md)创建它。

-   **启动关闭的调用。**

    客户端可以[发起传出呼叫关闭](client-initiated-request-to-close-a-call.md)做它接受的传入呼叫。

-   **查询或设置信息。**

    客户端可以查询或设置由绑定的呼叫管理器或 MCM 驱动程序的调用管理器部分维护的信息。 客户端还可以响应[查询，并设置](querying-or-setting-information.md)从绑定的呼叫管理器或 MCM 驱动程序。

    此外，客户端可以查询或设置由绑定的微型端口驱动程序或绑定的 MCM 驱动程序的微型端口驱动程序部分维护的信息。

-   **Inputsminiport 驱动程序状态指示。**

    客户端可以输入[所表示的面向连接的微型端口驱动程序状态](indicating-miniport-driver-status.md)或 MCM 驱动程序。

 

 





