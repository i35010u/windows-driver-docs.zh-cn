---
title: 处理 Microsoft Windows Sockets 扩展
description: 处理 Microsoft Windows Sockets 扩展
ms.assetid: e5209a63-519b-42bd-882b-a1c3d2074deb
keywords:
- 扩展 WDK Windows 套接字
- Windows 套接字直接 WDK，扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50495298a3e8c50da4ef00d0d51f42fb31d835bd
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218420"
---
# <a name="handling-microsoft-extensions-to-windows-sockets"></a>处理 Microsoft Windows Sockets 扩展





Windows 套接字交换机在内部处理所有 Microsoft 专用 Windows 套接字扩展功能。 Microsoft Windows SDK 中的 Windows 套接字文档将扩展定义为向应用程序公开高级传输功能的机制。 这些扩展函数包括： **TransmitFile**、 **AcceptEx**和 **GetAcceptExSockAddrs**。 此开关将在必要时转换这些调用，并将其转发到相应的 SAN 服务提供程序函数： [**WSPSend**](/previous-versions/windows/hardware/network/ff566316(v=vs.85))、 [**WSPAccept**](/previous-versions/windows/hardware/network/ff566266(v=vs.85))、 [**WSPRdmaWrite**](/previous-versions/windows/hardware/network/ff566306(v=vs.85))或 [**WSPRdmaRead**](/previous-versions/windows/hardware/network/ff566304(v=vs.85))。

 

