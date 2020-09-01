---
title: 在 SAN 上同步操作
description: 在 SAN 上同步操作
ms.assetid: 9bbceecc-652e-44a7-b969-57578d2ebe68
keywords:
- 同步 WDK San
- SAN 同步 WDK
- Windows 套接字直接 WDK，SAN 同步
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4689fc94567b828e6b6f60a4d49549749726167d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207155"
---
# <a name="synchronizing-operations-on-a-san"></a>在 SAN 上同步操作





Windows 套接字交换机使用其会话协议来处理 SAN 服务提供程序与应用程序之间的几乎所有同步。 也就是说，开关与 TCP/IP 提供程序一起处理应用程序中的大多数 **WSPAsyncSelect**、 **WSPEventSelect**和 **WSPSelect** 调用。 此开关不会将这些调用转发到 SAN 服务提供程序，除非指定 FD \_ ACCEPT 和 FD \_ 连接网络事件代码来调用 san 服务提供程序的 [**WSPEventSelect**](/previous-versions/windows/hardware/network/ff566287(v=vs.85)) 函数，如 [设置 san 连接](setting-up-a-san-connection.md)中所述。

 

