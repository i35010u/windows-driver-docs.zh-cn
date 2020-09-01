---
title: 完成数据传输请求
description: 完成数据传输请求
ms.assetid: 4c187202-c7a8-4fd8-984a-5bae647b74b0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb61af3353636731bce519be00ae2af5be200bf8
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216204"
---
# <a name="completing-data-transfer-requests"></a>完成数据传输请求





Windows 套接字交换机以异步方式在 SAN 套接字上传输数据。 每当开关调用 SAN 服务提供程序的 [**WSPSend**](/previous-versions/windows/hardware/network/ff566316(v=vs.85))、 [**WSPRecv**](/previous-versions/windows/hardware/network/ff566309(v=vs.85))、 [**WSPRdmaWrite**](/previous-versions/windows/hardware/network/ff566306(v=vs.85))或 [**WSPRdmaRead**](/previous-versions/windows/hardware/network/ff566304(v=vs.85)) 数据传输函数时，它都会指定一个指针，该指针指向 (WSAOVERLAPPED) 的重叠结构，并为完成例程指定 **NULL** 。 即使交换机调用 SAN 服务提供程序的 [**WSPEventSelect**](/previous-versions/windows/hardware/network/ff566287(v=vs.85)) 函数来指示套接字处于非阻止模式下，也不需要 SAN 服务提供程序来实现这些数据传输函数的非阻止语义。

如 Microsoft Windows SDK 文档中的 Windows 套接字 API 和 SPI 文档中所述，阻止和非阻止套接字将重叠操作视为相同。 也就是说，SAN 服务提供程序启动特定的数据传输操作，然后立即将控制权返回给该交换机。 这些数据传输函数返回错误代码 WSA \_ IO \_ 挂起，以指示异步操作已启动并且稍后会执行该操作。 操作完成后，如果交换机需要完成通知（如以下各段所述），则 SAN 服务提供程序将发出信号。

由于对于重叠数据传输操作的完成例程，开关始终指定 **NULL** ，因此，SAN 服务提供程序不需要通过使用 (apc) 的异步过程调用来支持完成。

如果可能，此开关将尝试调用 SAN 服务提供程序的 [**WSPGetOverlappedResult**](/previous-versions/windows/hardware/network/ff566288(v=vs.85)) 函数，以轮询数据传输请求是否已完成。 通过这种方式，开关可以避免与活动重叠完成机制关联的开销。 若要向 SAN 服务提供程序指示对于特定的重叠数据传输操作，开关不需要完成通知，则此开关会将[**WSAOVERLAPPED**](/previous-versions/windows/hardware/network/ff565952(v=vs.85))结构中的**hEvent**成员的低序位设置为1。 SAN 服务提供商不能通知此情况下提交的请求是否已完成。

如果开关需要通知已重叠的数据传输操作的完成，则它会将 WSAOVERLAPPED 结构中的 **hEvent** 成员的低序位设置为零。 SAN 服务提供程序必须通过调用 **WPUCompleteOverlappedRequest** 函数来完成以这种方式启动的数据传输操作。 在此调用中，SAN 服务提供程序将传递指向 WSAOVERLAPPED 结构的指针，该结构对应于已完成的数据传输操作。 在此 **WPUCompleteOverlappedRequest** 调用中，SAN 服务提供程序还将传递从开关获取的套接字描述符，并调用 **WPUCreateSocketHandle** 函数。 开关接收完成通知，将它们与应用程序的 i/o 请求相匹配，并根据应用程序的需要完成这些 i/o 请求。 有关 **WPUCompleteOverlappedRequest** 和 **WPUCreateSocketHandle** 函数的信息，请参阅 Windows SDK 文档。

 

