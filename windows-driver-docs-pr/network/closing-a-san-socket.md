---
title: 关闭 SAN 套接字
description: 关闭 SAN 套接字
keywords:
- SAN 套接字 WDK，关闭
- 关闭 SAN 套接字
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 859efcf6e6abb9c26ece7ec5ac93e254d4d29b1f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817639"
---
# <a name="closing-a-san-socket"></a>关闭 SAN 套接字





连接两侧的 Windows 套接字交换机调用 SAN 服务提供程序的 [**WSPCloseSocket**](/previous-versions/windows/hardware/network/ff566273(v=vs.85)) 函数后，san 服务提供程序将执行以下过程来关闭 SAN 套接字：

1.  连接两侧的每个 SAN 服务提供程序泪水连接，并通过在 *lpErrno* 参数中返回相应的错误代码来完成接收请求- [**WSPRecv**](/previous-versions/windows/hardware/network/ff566309(v=vs.85))函数调用。 例如，SAN 服务提供程序返回 WSAECONNRESET，以指示远程对等方重置连接。

    每个 SAN 服务提供商还会发出信号，使 SAN 套接字关闭挂起的重叠操作。 SAN 服务提供程序调用 **WPUCompleteOverlappedRequest** 函数来指示重叠操作的完成。 在此调用中，SAN 服务提供程序将传递指向与重叠操作关联的 [**WSAOVERLAPPED**](/previous-versions/windows/hardware/network/ff565952(v=vs.85)) 结构的指针。 SAN 服务提供程序还传递 WSA \_ 操作 \_ 中止错误代码，以指定由于 SAN 套接字已关闭而导致重叠操作被取消。 在完成重叠操作的通知完成前，SAN 服务提供程序应释放该操作所需的任何内存。

2.  在 SAN 服务提供商完成调用后（使用通过 **WPUCreateSocketHandle** 向上调用获得的 SAN 套接字的句柄）对带前缀 **WPU** 的函数进行调用时，san 服务提供程序必须通过调用 **WPUCloseSocketHandle** 函数以关闭套接字句柄，对开关进行最终向上调用。 然后，SAN 服务提供程序清除与 SAN 套接字相关的所有内容。 向上调用是从开关的向上调用调度表中调用的函数。 此开关在调用 SAN 服务提供程序的 [**WSPStartupEx**](/previous-versions/windows/hardware/network/ff566321(v=vs.85)) 函数开始使用提供程序时提供指向此向上调用调度表的指针。 有关这些向上调用函数的详细信息，请参阅 Microsoft Windows SDK 文档。

只要 SAN 服务提供商执行前面的过程来关闭 SAN 套接字，交换机就会负责其他所有操作。

若要防止 SAN 服务提供商和交换机启动套接字闭包之间出现争用情况，SAN 服务提供商应始终释放与 SAN 套接字相关的数据结构，直到交换机调用 **WSPCloseSocket**。

 

