---
title: 在 SAN 上的同步操作
description: 在 SAN 上的同步操作
ms.assetid: 9bbceecc-652e-44a7-b969-57578d2ebe68
keywords:
- 同步 WDK San
- SAN 同步 WDK
- Windows 套接字直接 WDK，SAN 同步
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94ad5101a5ccea0d64749fa9a5e53b628584c14b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541028"
---
# <a name="synchronizing-operations-on-a-san"></a>在 SAN 上的同步操作





Windows 套接字开关使用其会话协议来处理 SAN 服务提供商和应用程序之间的几乎所有同步。 中与 TCP/IP 提供程序，一起使用的交换机，即处理大多数**WSPAsyncSelect**， **WSPEventSelect**，并**WSPSelect**来自应用程序调用。 交换机将这些调用，除非指定 FD SAN 服务提供程序不转发\_ACCEPT 和 FD\_CONNECT 网络事件的代码调用到 SAN 服务提供商[ **WSPEventSelect**](https://msdn.microsoft.com/library/windows/hardware/ff566287)函数，如中所述[设置 SAN 连接](setting-up-a-san-connection.md)。

 

 





