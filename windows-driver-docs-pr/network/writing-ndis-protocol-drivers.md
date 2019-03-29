---
title: 编写 NDIS 协议驱动程序
description: 编写 NDIS 协议驱动程序
ms.assetid: 30d27b9b-e6b9-4548-ab83-f240e60d5393
keywords:
- 协议驱动程序 WDK 网络，有关协议驱动程序
- NDIS 协议驱动程序 WDK，有关协议的 NDIS 驱动程序
- NDIS 协议驱动程序 WDK、 写入
- 协议驱动程序 WDK 网络、 写入
- 编写 NDIS 协议驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0324bc86943bd0b00f3533107a26954b6dde5fe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576954"
---
# <a name="writing-ndis-protocol-drivers"></a>编写 NDIS 协议驱动程序





本文档提供的协议概述 NDIS 6.0 及更高版本的驱动程序操作。 协议的 NDIS 驱动程序提供*ProtocolXxx*函数的 NDIS 调用启动的操作。 提供了 NDIS **Ndis * Xxx*** 协议来执行操作的驱动程序调用的函数。

以下主题介绍绑定状态和操作之间的关系，以及包括某些协议驱动程序操作的概述：

-   [初始化协议驱动程序](initializing-a-protocol-driver.md)
-   [协议绑定状态和操作](protocol-binding-states-and-operations.md)
-   [绑定到适配器](binding-to-an-adapter.md)
-   [从适配器正在取消绑定](unbinding-from-an-adapter.md)
-   [启动和暂停绑定](starting-and-pausing-a-binding.md)
-   [配置可选的协议驱动程序服务](configuring-optional-protocol-driver-services.md)
-   [协议驱动程序发送和接收操作](protocol-driver-send-and-receive-operations.md)
-   [协议驱动程序 OID 请求](protocol-driver-oid-requests.md)
-   [处理状态指示在协议驱动程序](handling-status-indications-in-a-protocol-driver.md)
-   [协议驱动程序中处理即插即用事件通知](handling-pnp-event-notifications-in-a-protocol-driver.md)

 

 





