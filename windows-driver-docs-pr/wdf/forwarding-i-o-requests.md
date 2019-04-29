---
title: 转发 I/O 请求
description: 转发 I/O 请求
ms.assetid: 75e007e3-1b97-44db-ac86-56aab78222a6
keywords:
- 转发 I/O 请求 WDK KMDF
- I/O 请求 WDK KMDF，转发
- 请求处理 WDK KMDF、 转发 I/O 请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a29f2a7cb3e2e3072bb642cf4be5e4492d126ab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391351"
---
# <a name="forwarding-io-requests"></a>转发 I/O 请求





当驱动程序收到它无法处理的 I/O 请求时，它通常执行以下任一操作：

-   它会转发到另一个驱动程序收到的请求。

-   它创建额外的请求，并将其发送到另一个驱动程序。

基于框架的驱动程序将通过请求转发[使用 I/O 目标](using-i-o-targets.md)，表示系统上的其他驱动程序。 驱动程序可以使用任何以下方法将请求转发给 I/O 目标：

-   驱动程序可以通过调用转发到下一步低驱动程序的 I/O 请求[ **WdfDeviceGetIoTarget**](https://msdn.microsoft.com/library/windows/hardware/ff546017)后, 跟[ **WdfRequestFormatRequestUsingCurrentType**](https://msdn.microsoft.com/library/windows/hardware/ff549955)，并最后[ **WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)。

    此方法很有用，仅当该驱动程序收到不需要修改，然后再转发的请求。

-   驱动程序可以调用[ **WdfFdoInitSetFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff547273)将自身注册为筛选器驱动程序。

    如果筛选器驱动程序不提供有关特定类型的 I/O 请求的 I/O 队列，框架会自动将转发到下一步低驱动程序的该类型的请求。

-   通常情况下，功能驱动程序将检查每个 I/O 请求的内容。 如果功能驱动程序无法处理请求，它可能修改请求，并将其转发到 I/O 目标。 或者，它可能会创建一个或多个新的请求并将其发送到的 I/O 目标。

    框架的 I/O 目标对象定义用于将输入/输出请求发送到其他驱动程序的几种方法。 例如，驱动程序可以调用[ **WdfIoTargetFormatRequestForRead**](https://msdn.microsoft.com/library/windows/hardware/ff548612)后, 跟[ **WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)、 发送到的读取的请求I/O 目标。 有关 I/O 目标的详细信息，请参阅[使用 I/O 目标](using-i-o-targets.md)。

    很少，驱动程序编写者可能想要指定的内容的请求的基础 WDM [I/O 堆栈位置](https://msdn.microsoft.com/library/windows/hardware/ff551821)之前将请求发送到 I/O 的目标。 对于这些情况下，该驱动程序可调用[ **WdfRequestWdmFormatUsingStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550036)调用之前[ **WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)。

有时，驱动程序必须将发送同一请求到多个 I/O 目标，通常因为驱动程序必须将单个命令发送到所有其设备。 在将请求发送到的 I/O 目标之前, 驱动程序可以调用[ **WdfRequestChangeTarget** ](https://msdn.microsoft.com/library/windows/hardware/ff549943)若要验证的 I/O 目标是否可访问。

该驱动程序必须最终[完整](completing-i-o-requests.md)每个请求都转发到 I/O 的目标，除非它设置[ **WDF\_请求\_发送\_选项\_发送\_AND\_忘记**](https://msdn.microsoft.com/library/windows/hardware/ff552493)标志时调用[ **WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)。

请注意，当驱动程序将转发请求，框架不会不按原义 framework 请求对象从传输发送驱动程序到接收驱动程序。 相反，该框架在收到请求的驱动程序中创建一个新的请求对象。 仅在请求的基本 I/O 请求数据包 ([**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)) 从一个驱动程序传输到另一个。

 

 





