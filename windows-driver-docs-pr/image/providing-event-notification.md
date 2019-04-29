---
title: 提供事件通知
description: 提供事件通知
ms.assetid: 53ca7ef0-fa8b-4ae1-9b5e-b145c2d02db2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9651d28f798138c8ba78f67e18c0ed11f33732ab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379629"
---
# <a name="providing-event-notification"></a>提供事件通知





WIA 服务通知的受支持的设备事件 WIA 微型驱动程序通过调用[ **IWiaMiniDrv::drvNotifyPnpEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff544998)方法。 在此方法，微型驱动程序实现对事件作出响应所需的特定于设备的功能。 WIA 服务调用**IWiaMiniDrv::drvNotifyPnpEvent**方法只应该用于微型驱动程序已指明设备可以支持中的事件[ **IWiaMiniDrv::drvGetCapabilities**](https://msdn.microsoft.com/library/windows/hardware/ff543977)方法。

微型驱动程序启动事件时通过 STI 事件机制，或使用[ **wiasQueueEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff549296)若要将事件通知此设备添加到事件队列。

### <a name="asynchronous-behavior-power-management-and-io-cancellation"></a>异步行为：电源管理和 I/O 取消

在大多数情况下，WIA 服务可确保一次只有一个调用进行向驱动程序。 但是，某些方法是本质上是异步的、 在本质上可重入。 很好的例子是[ **IWiaMiniDrv::drvNotifyPnpEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff544998)方法。

WIA 服务使用此方法以通知可能需要立即采取措施的事件的驱动程序。 例如，如果 WIA 服务收到，该值指示已删除设备插事件时，它会通知驱动程序立即。 其他示例包括电源管理事件并从应用程序的 I/O 取消请求。

有关示例实现[ **IWiaMiniDrv::drvNotifyPnpEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff544998)方法，说明它应如何响应各种事件，请参阅[添加中断的事件支持](adding-interrupt-event-support.md).

 

 




