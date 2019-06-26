---
title: 完成数据传输请求
description: 完成数据传输请求
ms.assetid: 4c187202-c7a8-4fd8-984a-5bae647b74b0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0091e952a2abd64b190f53d4f231aa5c4a39ee83
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379251"
---
# <a name="completing-data-transfer-requests"></a>完成数据传输请求





Windows 套接字以异步方式切换 SAN 套接字上的传输数据。 每当此开关调用 SAN 服务提供商[ **WSPSend**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566316(v=vs.85))， [ **WSPRecv**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566309(v=vs.85))， [ **WSPRdmaWrite**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566306(v=vs.85))，或[ **WSPRdmaRead** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566304(v=vs.85))数据传输函数，它指定一个指向重叠的结构 (WSAOVERLAPPED) 和**NULL**完成例程。 即使此开关调用 SAN 服务提供商[ **WSPEventSelect** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566287(v=vs.85))函数来指示套接字处于未锁定模式、 SAN 服务提供程序不需要实现非阻止性这些数据传输函数的语义。

Microsoft Windows SDK 文档中的 Windows 套接字 API 和 SPI 文档中所述，阻塞和非阻止性套接字将重叠的操作相同。 也就是说，SAN 服务提供商启动特定的数据传输操作，并再立即将控制权返回到该交换机。 这些数据传输函数将返回错误代码 WSA\_IO\_PENDING 指示异步操作已启动并完成该操作的更高版本发生。 在操作完成后，SAN 服务提供程序将指示完成如果开关需要完成通知，如以下各段中所述。

因为开关始终指定**NULL** SAN 服务提供商不重叠的数据传输操作的完成例程，对于需要支持通过使用异步过程调用 (Apc) 完成。

只要有可能，尝试调用 SAN 服务提供商的开关[ **WSPGetOverlappedResult** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566288(v=vs.85))函数来轮询完成状态的数据传输请求。 这样一来，此开关可以避免与活动的重叠的完成机制相关的开销。 若要指示 SAN 服务提供商开关不要求对特定重叠的数据传输操作完成通知，此开关设置的低顺序位**hEvent**中的成员[ **WSAOVERLAPPED** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565952(v=vs.85))到一个结构。 SAN 服务提供商必须不通知以这种方式提交的请求完成的开关。

如果此开关需要重叠的数据传输操作完成通知的则将设置的低顺序位**hEvent**为零 WSAOVERLAPPED 结构中的成员。 SAN 服务提供商必须完成的数据传输操作中这种方式启动通过调用**WPUCompleteOverlappedRequest**完成信号函数。 在此调用中，SAN 服务提供商将指针传递给 WSAOVERLAPPED 结构，它对应于已完成的数据传输操作中。 在此**WPUCompleteOverlappedRequest**调用，SAN 服务提供程序还将传递已获取的套接字描述符从调用中的交换机**WPUCreateSocketHandle**函数。 此开关接收完成通知，它们与应用程序的 I/O 请求，并完成这些 I/O 请求，根据需要，为应用程序。 璝惠**WPUCompleteOverlappedRequest**并**WPUCreateSocketHandle**函数，请参阅 Windows SDK 文档。

 

 





