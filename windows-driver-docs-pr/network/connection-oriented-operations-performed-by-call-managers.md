---
title: 呼叫管理程序执行的面向连接的操作
description: 呼叫管理程序执行的面向连接的操作
ms.assetid: 6df23eb2-df02-4d24-88b3-c02b87edb38b
keywords:
- 面向连接的 NDIS WDK，调用管理器
- CoNDIS WDK 网络、 调用管理器
- 调用管理器 WDK 网络、 面向连接的操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7025de9d07fc53fbeacbb66112366389992b8e2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357529"
---
# <a name="connection-oriented-operations-performed-by-call-managers"></a>呼叫管理程序执行的面向连接的操作





呼叫管理器执行：

-   **进行注册和注销一个或多个地址系列 (AFs)。**

    呼叫管理器[注册一个或多个地址系列](registering-and-opening-an-address-family.md)使用 NDIS。 通过注册地址族，呼叫管理器会通告其调用管理器服务 （具体而言，信号传输协议） 绑定的面向连接的客户端。 使用 NDIS 注册入口点的相关信息，请参阅[CoNDIS 注册](condis-registration.md)。

-   **进行注册和注销 SAPs 的面向连接的客户端请求。**

    呼叫管理器接收到的绑定的面向连接的客户端的请求[注册 SAPs](registering-a-sap.md)进出[取消注册 SAPs](deregistering-a-sap.md)。 调用管理器发送信号以注册或取消注册 SAPs 代表客户端在网络上的消息。

-   **设置的面向连接的客户端请求的传出调用。**

    当面向连接的客户端[进行传出调用](making-a-call.md)，呼叫管理器根据需要，建立的与网络控制设备通信 （信号消息交换）。 如果远程方呼叫管理器接受在调用[激活 VC](activating-a-vc.md)为调用创建的。

-   **设置并指示对面向连接的客户端的传入呼叫。**

    呼叫管理器指示绑定的面向连接的客户端发送到由该客户端注册 SAP 的所有调用。 之前[，该值指示传入呼叫](indicating-an-incoming-call.md)向客户端，调用管理器会启动[VC 创建](creating-a-vc.md)的调用然后启动[VC 激活](activating-a-vc.md)。

-   **进行通信的 QoS 的更改请求。**

    呼叫管理器可以根据信号协议进行通信[从本地客户端的请求以更改传出或传入调用的 QoS](client-initiated-request-to-change-call-parameters.md)或[从远程方请求更改为调用QoS](incoming-request-to-change-call-parameters.md).

-   **进行通信来添加和删除参与方的请求。**

    调用管理器通信，对本地客户端的请求[添加的参与方](adding-a-party-to-a-multipoint-call.md)到或[删除参与方](dropping-a-party-from-a-multipoint-call.md)从点到多点调用。 呼叫管理器也能远程方进行通信[传入请求，从点 multipoint 调用 drop 本身](incoming-request-to-drop-a-party-from-a-multipoint-call.md)。

-   **向下调用得流泪。**

    在面向连接的客户端请求时，调用管理器关闭调用通过网络控制设备对与通信[终止的连接](client-initiated-request-to-close-a-call.md)。 在远程方请求时，呼叫管理器指示本地面向连接的客户端到远程方[关闭调用请求](incoming-request-to-close-a-call.md)。 在过程中关闭的调用，呼叫管理器[停用 VC](deactivating-a-vc.md)中所用的调用。 如果呼叫管理器创建 VC （用于传入呼叫），还可以呼叫管理器[删除 VC](deleting-a-vc.md)。

-   **查询或设置信息。**

    呼叫管理器可以[查询或设置信息](querying-or-setting-information.md)由绑定的面向连接的客户端维护。 呼叫管理器还可以响应来查询和设置从绑定的面向连接的客户端的操作。

    此外，呼叫管理器可使用查询或设置绑定的微型端口驱动程序或通过绑定 MCM 驱动程序的微型端口驱动程序部分维护的信息。

-   **Inputsminiport 驱动程序状态指示。**

    调用管理器输入[来自绑定的面向连接的微型端口驱动程序的状态指示](indicating-miniport-driver-status.md)。

 

 





