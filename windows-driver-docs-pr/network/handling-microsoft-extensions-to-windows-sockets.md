---
title: 处理 Microsoft Windows Sockets 扩展
description: 处理 Microsoft Windows Sockets 扩展
keywords:
- 扩展 WDK Windows 套接字
- Windows 套接字直接 WDK，扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 627a14adb73f39bae4fb10205adac3ddabffa40e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802361"
---
# <a name="handling-microsoft-extensions-to-windows-sockets"></a>处理 Microsoft Windows Sockets 扩展





Windows 套接字交换机在内部处理所有 Microsoft 专用 Windows 套接字扩展功能。 Microsoft Windows SDK 中的 Windows 套接字文档将扩展定义为向应用程序公开高级传输功能的机制。 这些扩展函数包括： **TransmitFile**、 **AcceptEx** 和 **GetAcceptExSockAddrs**。 此开关将在必要时转换这些调用，并将其转发到相应的 SAN 服务提供程序函数： [**WSPSend**](/previous-versions/windows/hardware/network/ff566316(v=vs.85))、 [**WSPAccept**](/previous-versions/windows/hardware/network/ff566266(v=vs.85))、 [**WSPRdmaWrite**](/previous-versions/windows/hardware/network/ff566306(v=vs.85))或 [**WSPRdmaRead**](/previous-versions/windows/hardware/network/ff566304(v=vs.85))。

 

