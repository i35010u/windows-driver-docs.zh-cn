---
title: 微型端口驱动程序执行的面向连接的操作
description: 微型端口驱动程序执行的面向连接的操作
ms.assetid: c49f93b2-6a51-45b6-8b02-93f3bef8dcde
keywords:
- 微型端口驱动程序 WDK 网络的 CoNDIS
- 面向连接的 NDIS WDK，微型端口驱动程序
- CoNDIS WDK 网络、 微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42078edf0f0dde9167fb25284cb7eb15b1156513
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564046"
---
# <a name="connection-oriented-operations-performed-by-miniport-drivers"></a>微型端口驱动程序执行的面向连接的操作





除了控制 NIC 硬件，面向连接的微型端口驱动程序：

-   **发送和接收数据包。**

    面向连接的微型端口驱动程序发送和接收数据包代表面向连接的客户端或调用管理器。

-   **创建 （设置） VCs。**

    在面向连接的客户端，面向连接的微型端口驱动程序的请求时[分配并初始化为 VC 资源](creating-a-vc.md)对于传出呼叫。 在呼叫管理器请求时，面向连接的微型端口驱动程序分配，并为 VC 用于传入呼叫或接收的发送呼叫管理器将初始化资源信号消息。

-   **激活 VCs。**

    在呼叫管理器请求时，面向连接的微型端口驱动程序与 NIC 以准备要接收或在 VC 上传输数据的 NIC 进行通信 (请参阅[激活 VC](activating-a-vc.md))。

-   **VCs 将停用。**

    在呼叫管理器请求时，面向连接的微型端口驱动程序与 NIC 以跨 VC 终止所有通信进行通信 (请参阅[停用 VC](deactivating-a-vc.md))。

-   **删除 VCs。**

    在面向连接的客户端请求时，面向连接的微型端口驱动程序将为其创建由该客户端启动的 VC 释放资源 (请参阅[删除 VC](deleting-a-vc.md))。 在呼叫管理器请求时，面向连接的微型端口驱动程序为其创建由该呼叫管理器启动 VC 释放资源。

-   **响应信息的查询或设置。**

    面向连接的微型端口驱动程序响应[查询和设置操作](querying-or-setting-information.md)由绑定的面向连接的客户端或调用管理器。

-   **指示状态。**

    面向连接的微型端口驱动程序可以[指示其状态或 NIC 的状态中的变化](indicating-miniport-driver-status.md)绑定面向连接的客户端和呼叫管理器。

-   **重置 NIC**

    在 NDIS，面向连接的微型端口驱动程序的请求时[重置](reset.md)nic。

 

 





