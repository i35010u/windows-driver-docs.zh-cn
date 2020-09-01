---
title: 确定当前的连接卸载设置
description: 确定当前的连接卸载设置
ms.assetid: aca377ae-c56b-4f84-8165-4b084bfa9938
keywords:
- 连接卸载 WDK TCP/IP 传输，当前设置
- 当前连接卸载设置 WDK TCP/IP 卸载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc015bd0900bfea28b4471f18f2e59a3f989db1d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212935"
---
# <a name="determining-the-current-connection-offload-settings"></a>确定当前的连接卸载设置





协议驱动程序可以使用对象标识符 (OID) 请求获取连接卸载服务。

若要获取网络接口卡的当前连接卸载设置 (NIC) ，协议驱动程序可以查询 [oid \_ TCP \_ 连接 \_ 卸载 \_ 参数](./oid-tcp-connection-offload-parameters.md) OID。

 

