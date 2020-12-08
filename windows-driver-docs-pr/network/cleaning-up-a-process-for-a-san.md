---
title: 清理 SAN 的进程
description: 清理 SAN 的进程
keywords:
- SAN process 清理 WDK
- 清理 SAN 进程 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05a5628d78606ffe207086fd37dee1cd381f15d1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826975"
---
# <a name="cleaning-up-a-process-for-a-san"></a>清理 SAN 的进程





当应用程序准备好清理正在运行的进程时，它将启动对 Windows 套接字交换机的 **WSPCleanup** 函数的调用。 交换机又调用 TCP/IP 提供程序和所有 SAN 服务提供程序的 [**WSPCleanup**](/previous-versions/windows/hardware/network/ff566270(v=vs.85)) 函数。 所有提供程序都应释放它们正在使用的所有资源。 例如，资源可以包含用于同步事件的对象，以及用于执行数据传输的内存。

 

