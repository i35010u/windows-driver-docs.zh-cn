---
title: 配置端口
description: 配置端口
ms.assetid: f5996e94-aa48-4aa0-82f5-331a57d2fb6b
keywords:
- 端口管理 WDK 打印、 配置端口
- ConfigurePort
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8407e96d073b73556cfe1f50abc7683ee91fb95b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565290"
---
# <a name="configuring-a-port"></a>配置端口





配置的端口包括修改之前添加端口的端口监视器服务器 DLL 的存储的配置信息。

当应用程序调用打印后台处理程序的[ **ConfigurePort** ](https://msdn.microsoft.com/library/windows/hardware/ff546286)函数 （Microsoft Windows SDK 文档中介绍）， **ConfigurePort**函数调用[ **ConfigurePortUI** ](https://msdn.microsoft.com/library/windows/hardware/ff546290)端口监视器 UI DLL 的适当的端口监视器中包含的函数。

端口监视器 UI DLL 的[ **ConfigurePortUI** ](https://msdn.microsoft.com/library/windows/hardware/ff546290)函数应执行以下操作：

1.  调用打印后台处理程序的 OpenPrinter 函数 （Windows SDK 文档中介绍），这会导致[ **XcvOpenPort** ](https://msdn.microsoft.com/library/windows/hardware/ff564259)中端口监视服务器 DLL 调用的函数。

2.  调用打印后台处理程序的[ **XcvData** ](https://msdn.microsoft.com/library/windows/hardware/ff564255)函数的一个或多个时间，以 UI DLL 和 DLL 的服务器之间传输的配置信息。 **XcvData**函数将调用服务器 DLL 的[ **XcvDataPort** ](https://msdn.microsoft.com/library/windows/hardware/ff564258)函数。 [ **ConfigurePortUI** ](https://msdn.microsoft.com/library/windows/hardware/ff546290)函数通常可获取配置信息从用户的显示对话框。

3.  调用打印后台处理程序的 ClosePrinter 函数 （Windows SDK 文档中介绍），这会导致[ **XcvClosePort** ](https://msdn.microsoft.com/library/windows/hardware/ff564254)中端口监视服务器 DLL 调用的函数。

有关这些操作的详细信息，请参阅的说明[ **ConfigurePortUI**](https://msdn.microsoft.com/library/windows/hardware/ff546290)。 另请参阅[存储端口的配置信息](storing-port-configuration-information.md)。

 

 




