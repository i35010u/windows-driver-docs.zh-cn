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
ms.openlocfilehash: d2a130eaf4fc665f390cfb90b9f9af2b0b31572d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824778"
---
# <a name="adding-bidirectional-communication"></a>添加双向通信





后台处理程序支持应用程序或驱动程序与打印机之间的双向（"双向"）通信。 此支持使应用程序或驱动程序可以将一个或多个请求发送到打印机，并使打印机能够对这些请求进行响应。

![演示双向支持体系结构的关系图](images/bidi.png)

### <a name="bidirectional-communication-requirements"></a>双向通信要求

在应用程序或驱动程序可以使用双向通信之前，它必须实现[双向通信接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)： IBidiSpl com 接口或 IbidiSpl2 com 接口，以及至少一个 IBidiRequest 和IBidiRequestContainer COM 接口。 此外，还必须满足以下一项或两项条件：

-   [**SendRecvBidiData**](https://docs.microsoft.com/previous-versions/ff562068(v=vs.85))函数在打印提供程序 DLL 中实现。

-   在语言监视服务器 DLL 或端口监视器服务器 DLL 中实现[**SendRecvBidiDataFromPort**](https://docs.microsoft.com/previous-versions/ff562071(v=vs.85))函数。

若要向打印机发送单个请求，应用程序或打印机驱动程序必须首先编写请求，然后调用 IBidiSpl：： SendRecv 方法。 若要发送多个请求，应用程序或驱动程序将撰写请求列表，然后调用 IBidiSpl：： MultiSendRecv 方法。

收到请求后，后台处理程序的客户端部分（Winspool.drv）会将其传递到服务器端后台处理程序（spoolsv.exe）。 服务器端后台处理程序可以位于本地计算机上，也可以位于远程网络打印服务器上。 当服务器端后台处理程序收到请求时，它会分析请求中的数据，并填写[**双向\_请求的成员\_容器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winspool/ns-winspool-_bidi_request_container)结构。 服务器端后台处理程序会调用[**SendRecvBidiData**](https://docs.microsoft.com/previous-versions/ff562068(v=vs.85))或[**SendRecvBidiDataFromPort**](https://docs.microsoft.com/previous-versions/ff562071(v=vs.85))。 当任一函数返回时，其*ppResData*参数会指向一个内存位置，该内存位置包含已填充的[**双向\_响应\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/winspool/ns-winspool-_bidi_response_container)包含打印机响应的容器结构。 服务器端后台处理程序将此结构中的数据转换为适合应用程序或驱动程序使用的形式，并将其传递回客户端后台处理程序，最后返回到请求的发起方。

 

 




