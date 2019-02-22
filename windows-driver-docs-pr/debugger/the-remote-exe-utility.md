---
title: Remote.exe 实用程序
description: Remote.exe 实用程序
ms.assetid: 3780d632-939e-4adb-82f1-fd7c25706b54
keywords:
- remote.exe，remote.exe 实用程序通过远程调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6dc26101fbe58a0d1d95abc0fd9801e1666d7a21
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546107"
---
# <a name="the-remoteexe-utility"></a>Remote.exe 实用程序


## <span id="ddk_the_remote_exe_utility_dbg"></span><span id="DDK_THE_REMOTE_EXE_UTILITY_DBG"></span>


Remote.exe 实用工具是一个通用的服务器/客户端工具，可用于远程计算机上运行命令行程序。

Remote.exe 通过命名管道进行输入和输出使用 STDIN 和 STDOUT 的应用程序提供远程网络的访问。 在网络上的其他计算机的用户或通过直接拨号调制解调器连接来连接。 可以查看远程会话或输入命令本身。

此实用程序具有大量使用。 例如，当正在开发软件时在计算机上执行其他任务, 可以编译代码使用的处理器和远程计算机的资源。 Remote.exe 还可用于在多台计算机分发特定任务的处理要求。

请注意该 remote.exe 没有安全授权，并将允许任何人运行 Remote.exe 客户端连接到 Remote.exe 服务器。 这将使 Remote.exe 服务器运行打开到的任何用户连接的帐户。

 

 





