---
title: 关闭 SAN 套接字
description: 关闭 SAN 套接字
ms.assetid: 49224987-ed46-4631-a47b-70cd855cfa40
keywords:
- SAN 套接字 WDK，关闭
- 关闭 SAN 套接字
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13b2c15d4efaa08a2347686c7390edd36acf1c17
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564706"
---
# <a name="closing-a-san-socket"></a>关闭 SAN 套接字





连接的任何一侧切换 Windows 套接字后调用 SAN 服务提供商[ **WSPCloseSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff566273)函数，SAN 服务提供程序执行以下步骤来关闭 SAN 套接字:

1.  连接的任何一侧上每个 SAN 服务提供程序关闭连接并完成接收请求- [ **WSPRecv** ](https://msdn.microsoft.com/library/windows/hardware/ff566309)通过返回相应的错误代码在函数调用-*lpErrno*参数。 例如，SAN 服务提供程序返回 WSAECONNRESET 以指示远程对等方重置该连接。

    每个 SAN 服务提供商还向发出信号挂起的 SAN 套接字要关闭的重叠操作的完成。 SAN 服务提供程序调用**WPUCompleteOverlappedRequest**重叠操作的完成信号函数。 在此调用中，SAN 服务提供商将传递一个指向[ **WSAOVERLAPPED** ](https://msdn.microsoft.com/library/windows/hardware/ff565952)与重叠的操作相关联的结构。 SAN 服务提供程序还将传递 WSA\_操作\_已中止错误代码，以指定重叠的操作已取消，因为 SAN 套接字已关闭。 信号重叠操作完成之前, SAN 服务提供商应释放操作所需的任何内存。

2.  SAN 服务提供商进行最多的调用-在完成后调用的函数时，都带有前缀**WPU**-到使用句柄通过获得的 SAN 套接字交换机**WPUCreateSocketHandle**最多调用，SAN 服务提供商必须使最后的向上调用到交换机通过调用**WPUCloseSocketHandle**函数以关闭套接字句柄。 SAN 服务提供商，然后清理到 SAN 套接字相关的所有内容。 最多调用是将开关的最多调用调度表中的函数调用。 该交换机提供指向此向上调用调度表时调用 SAN 服务提供商[ **WSPStartupEx** ](https://msdn.microsoft.com/library/windows/hardware/ff566321)函数以开始使用该提供程序。 有关这些向上调用函数的详细信息，请参阅 Microsoft Windows SDK 文档。

只要 SAN 服务提供程序执行前面的过程，以关闭 SAN 套接字，交换机将负责其他所有内容。

若要防止 SAN 服务提供程序和启动套接字闭包的交换机之间的争用条件，SAN 服务提供程序应永远不会释放到 SAN 套接字相关直到开关调用的数据结构**WSPCloseSocket**。

 

 





