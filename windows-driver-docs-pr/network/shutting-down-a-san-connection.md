---
title: 关闭 SAN 连接
description: 关闭 SAN 连接
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40b668fc406c7d6f3531c2e36e4033a37b04ddcd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829159"
---
# <a name="shutting-down-a-san-connection"></a>关闭 SAN 连接





Windows 套接字交换机使用其会话协议关闭到 SAN 套接字的连接。 也就是说，该开关处理应用程序中的 **WSPRecvDisconnect**、 **WSPSendDisconnect** 和 **WSPShutdown** 调用。 此开关不会将这些调用转发到 SAN 服务提供程序。 交换机使用其会话协议禁用在 SAN 套接字上接收和传输数据。

 

 





