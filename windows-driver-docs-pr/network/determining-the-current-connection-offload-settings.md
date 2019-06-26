---
title: 确定当前的连接卸载设置
description: 确定当前的连接卸载设置
ms.assetid: aca377ae-c56b-4f84-8165-4b084bfa9938
keywords:
- 连接将卸载 WDK TCP/IP 传输，当前设置
- 当前连接的卸载的设置 WDK TCP/IP 卸载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2b11a46fa7702715d332ded4994644ac21770f7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353353"
---
# <a name="determining-the-current-connection-offload-settings"></a>确定当前的连接卸载设置





协议驱动程序可以获取连接卸载服务使用的对象标识符 (OID) 请求。

若要获取当前连接的网络接口卡 (NIC) 的卸载设置，协议驱动程序可以查询[OID\_TCP\_连接\_卸载\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-parameters)OID。

 

 





