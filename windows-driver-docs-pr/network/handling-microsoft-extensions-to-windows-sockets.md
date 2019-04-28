---
title: 处理 Microsoft Windows Sockets 扩展
description: 处理 Microsoft Windows Sockets 扩展
ms.assetid: e5209a63-519b-42bd-882b-a1c3d2074deb
keywords:
- 扩展 WDK Windows 套接字
- Windows 套接字直接 WDK 扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 791e61956ea3374e2acf6dfba727263bcf926835
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330877"
---
# <a name="handling-microsoft-extensions-to-windows-sockets"></a>处理 Microsoft Windows Sockets 扩展





Windows 套接字开关会在内部处理所有特定于 Microsoft 的 Windows 套接字扩展函数。 Microsoft Windows SDK 中的文档定义的扩展，如公开一种机制高级 Windows 套接字传输到应用程序的功能。 这些扩展功能如下：**TransmitFile**， **AcceptEx**，和**GetAcceptExSockAddrs**。 交换机将这些调用，转换根据需要，并将其转发到适当的 SAN 服务提供程序函数：[**WSPSend**](https://msdn.microsoft.com/library/windows/hardware/ff566316)， [ **WSPAccept**](https://msdn.microsoft.com/library/windows/hardware/ff566266)， [ **WSPRdmaWrite**](https://msdn.microsoft.com/library/windows/hardware/ff566306)，或[ **WSPRdmaRead**](https://msdn.microsoft.com/library/windows/hardware/ff566304)。

 

 





