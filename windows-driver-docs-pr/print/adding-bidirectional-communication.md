---
title: 添加双向通信
description: 添加双向通信
ms.assetid: 30767eda-e456-4928-afac-40edd2ab48fc
keywords:
- 打印后台处理程序自定义 WDK，双向通信
- 后台处理程序自定义 WDK 打印，双向通信
- 自定义打印后台处理程序组件 WDK，双向通信
- 双向通信 WDK 打印
- 双向通信 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d750f24c78370ecc83d2401dbc2d57d0db034b34
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343168"
---
# <a name="adding-bidirectional-communication"></a>添加双向通信





后台处理程序的应用程序或驱动程序与打印机之间的双向 （"双向"） 通信提供支持。 这种支持使得应用程序或驱动程序将一个或多个请求发送到打印机和打印机响应这些请求。

![说明双向支持体系结构的关系图](images/bidi.png)

### <a name="bidirectional-communication-requirements"></a>双向通信要求

应用程序或驱动程序可以使用 bidi 通信之前，它必须实现[双向通信接口](https://msdn.microsoft.com/library/windows/hardware/ff545163): IBidiSpl COM 接口或 IbidiSpl2 COM 接口，以及至少一个IBidiRequest 和 IBidiRequestContainer COM 接口。 此外，必须满足一个或两个以下：

-   [ **SendRecvBidiData** ](https://msdn.microsoft.com/library/windows/hardware/ff562068)打印提供程序 DLL 中实现函数。

-   [ **SendRecvBidiDataFromPort** ](https://msdn.microsoft.com/library/windows/hardware/ff562071)语言监视器服务器动态链接库或端口监视器服务器 DLL 中实现函数。

若要将单个请求发送到打印机，应用程序或打印机的驱动程序必须首先编写请求，然后调用 IBidiSpl::SendRecv 方法。 若要发送多个请求，应用程序或驱动程序组合的请求，列表，然后调用 IBidiSpl::MultiSendRecv 方法。

收到请求后，后台处理程序 (Winspool.drv) 的客户端的部分将其传递到服务器端的后台处理程序 (spoolsv.exe)。 服务器端的后台处理程序可以是本地计算机上或远程网络打印服务器上。 当服务器端的后台处理程序收到请求时，它将分析该请求中的数据并填充中的成员[ **BIDI\_请求\_容器**](https://msdn.microsoft.com/library/windows/hardware/ff545193)结构。 然后，服务器端的后台处理程序调用[ **SendRecvBidiData** ](https://msdn.microsoft.com/library/windows/hardware/ff562068)或[ **SendRecvBidiDataFromPort**](https://msdn.microsoft.com/library/windows/hardware/ff562071)。 当任何一个函数返回时，其*ppResData*参数指向包含填充的程序的地址的内存位置[ **BIDI\_响应\_容器**](https://msdn.microsoft.com/library/windows/hardware/ff545202)结构，它包含打印机的响应。 服务器端的后台处理程序将此结构中的数据转换为适用于使用的窗体，由应用程序或驱动程序，并将其传递回客户端的后台处理程序，最后返回到请求的发起。

 

 




