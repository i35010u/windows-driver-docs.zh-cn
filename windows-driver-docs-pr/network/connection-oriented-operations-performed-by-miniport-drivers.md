---
title: 微型端口驱动程序执行的面向连接的操作
description: 微型端口驱动程序执行的面向连接的操作
keywords:
- 微型端口驱动程序 WDK 网络，CoNDIS
- 面向连接的 NDIS WDK，微型端口驱动程序
- CoNDIS WDK 网络，微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b51867d7540217bb8173514dab743cb9396b4c44
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813707"
---
# <a name="connection-oriented-operations-performed-by-miniport-drivers"></a>微型端口驱动程序执行的面向连接的操作





除了控制 NIC 硬件外，还可以使用面向连接的微型端口驱动程序：

-   **发送和接收数据包。**

    面向连接的微型端口驱动程序代表面向连接的客户端或呼叫管理器来发送和接收数据包。

-   **创建) VCs (设置。**

    在面向连接的客户端发出请求时，面向连接的微型端口驱动程序为传出调用 [分配和初始化用于 VC 的资源](creating-a-vc.md) 。 呼叫管理器请求时，面向连接的微型端口驱动程序为传入呼叫分配和初始化 VC 的资源，或调用管理器将在其上发送或接收信号消息的资源。

-   **激活 VCs。**

    呼叫管理器请求时，面向连接的微型端口驱动程序与 NIC 通信，以便准备 NIC 以在 VC 中接收或传输数据 (请参阅 [激活 vc](activating-a-vc.md)) 。

-   **停用 VCs。**

    呼叫管理器请求时，面向连接的微型端口驱动程序与 NIC 通信，以终止所有通过 VC (通信，请参阅 [停用 vc](deactivating-a-vc.md)) 。

-   **删除 VCs。**

    在面向连接的客户端发出请求时，面向连接的微型端口驱动程序会释放由该客户端启动的 VC 的资源， (参阅 [删除 vc](deleting-a-vc.md)) 。 呼叫管理器请求时，面向连接的微型端口驱动程序会释放由该调用管理器启动的 VC 的资源。

-   **响应信息查询或集。**

    面向连接的微型端口驱动程序通过绑定的面向连接的客户端或调用管理器响应 [查询和设置操作](querying-or-setting-information.md) 。

-   **指示状态。**

    面向连接的微型端口驱动程序可以 [指示其状态更改或 NIC](indicating-miniport-driver-status.md) 到绑定连接的客户端和调用管理器的状态的更改。

-   **重置 NIC。**

    当 NDIS 请求时，面向连接的微型端口驱动程序会 [重置](reset.md) NIC。

 

 





