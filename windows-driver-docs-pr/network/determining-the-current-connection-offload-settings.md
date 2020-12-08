---
title: 确定当前的连接卸载设置
description: 确定当前的连接卸载设置
keywords:
- 连接卸载 WDK TCP/IP 传输，当前设置
- 当前连接卸载设置 WDK TCP/IP 卸载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98a721d79927c4206f7e881c8bff4f2259300c8e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808667"
---
# <a name="determining-the-current-connection-offload-settings"></a>确定当前的连接卸载设置





协议驱动程序可以使用对象标识符 (OID) 请求获取连接卸载服务。

若要获取网络接口卡的当前连接卸载设置 (NIC) ，协议驱动程序可以查询 [oid \_ TCP \_ 连接 \_ 卸载 \_ 参数](./oid-tcp-connection-offload-parameters.md) OID。

 

