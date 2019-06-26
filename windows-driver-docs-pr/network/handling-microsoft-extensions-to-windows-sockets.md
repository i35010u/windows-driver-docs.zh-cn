---
title: 处理 Microsoft Windows Sockets 扩展
description: 处理 Microsoft Windows Sockets 扩展
ms.assetid: e5209a63-519b-42bd-882b-a1c3d2074deb
keywords:
- 扩展 WDK Windows 套接字
- Windows 套接字直接 WDK 扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0e743ba1a6d6fbae705b5783e491f89a007f6a4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379821"
---
# <a name="handling-microsoft-extensions-to-windows-sockets"></a>处理 Microsoft Windows Sockets 扩展





Windows 套接字开关会在内部处理所有特定于 Microsoft 的 Windows 套接字扩展函数。 Microsoft Windows SDK 中的文档定义的扩展，如公开一种机制高级 Windows 套接字传输到应用程序的功能。 这些扩展功能如下：**TransmitFile**， **AcceptEx**，和**GetAcceptExSockAddrs**。 交换机将这些调用，转换根据需要，并将其转发到适当的 SAN 服务提供程序函数：[**WSPSend**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566316(v=vs.85))， [ **WSPAccept**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566266(v=vs.85))， [ **WSPRdmaWrite**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566306(v=vs.85))，或[ **WSPRdmaRead**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566304(v=vs.85))。

 

 





