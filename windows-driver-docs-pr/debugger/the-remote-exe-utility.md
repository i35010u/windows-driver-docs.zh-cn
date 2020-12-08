---
title: Remote.exe 实用工具
description: Remote.exe 实用工具
keywords:
- 通过 remote.exe remote.exe 实用工具进行远程调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e877f2555408ef5a34f9b60461ebb8fa73a63bf0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795641"
---
# <a name="the-remoteexe-utility"></a>Remote.exe 实用工具


## <span id="ddk_the_remote_exe_utility_dbg"></span><span id="DDK_THE_REMOTE_EXE_UTILITY_DBG"></span>


remote.exe 实用程序是一种用于在远程计算机上运行命令行程序的通用服务器/客户端工具。

Remote.exe 通过将命名管道传递到使用 STDIN 和 STDOUT 进行输入和输出的应用程序，提供远程网络访问。 网络上其他计算机上的用户，或通过直接拨号调制解调器连接进行连接的用户。 可以查看远程会话或输入命令本身。

此实用程序的使用数量很多。 例如，在开发软件时，你可以在计算机上执行其他任务时使用远程计算机的处理器和资源编译代码。 你还可以使用 remote.exe 将特定任务的处理要求分散到多台计算机上。

请注意，remote.exe 不会进行安全授权，并允许运行 Remote.exe 客户端的任何人连接到 Remote.exe 服务器。 这会使 Remote.exe 服务器运行时所用的帐户对连接的任何人开放。

 

 





