---
title: 配置端口
description: 配置端口
ms.assetid: f5996e94-aa48-4aa0-82f5-331a57d2fb6b
keywords:
- 端口管理 WDK 打印、 配置端口
- ConfigurePort
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1a00ee45aab2f46107444d67d832a259ac86889
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379707"
---
# <a name="configuring-a-port"></a>配置端口





配置的端口包括修改之前添加端口的端口监视器服务器 DLL 的存储的配置信息。

当应用程序调用打印后台处理程序的[ **ConfigurePort** ](https://docs.microsoft.com/previous-versions/ff546286(v=vs.85))函数 （Microsoft Windows SDK 文档中介绍）， **ConfigurePort**函数调用[ **ConfigurePortUI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-configureportui)端口监视器 UI DLL 的适当的端口监视器中包含的函数。

端口监视器 UI DLL 的[ **ConfigurePortUI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-configureportui)函数应执行以下操作：

1.  调用打印后台处理程序的 OpenPrinter 函数 （Windows SDK 文档中介绍），这会导致[ **XcvOpenPort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-xcvopenport)中端口监视服务器 DLL 调用的函数。

2.  调用打印后台处理程序的[ **XcvData** ](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))函数的一个或多个时间，以 UI DLL 和 DLL 的服务器之间传输的配置信息。 **XcvData**函数将调用服务器 DLL 的[ **XcvDataPort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-xcvdataport)函数。 [ **ConfigurePortUI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-configureportui)函数通常可获取配置信息从用户的显示对话框。

3.  调用打印后台处理程序的 ClosePrinter 函数 （Windows SDK 文档中介绍），这会导致[ **XcvClosePort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-xcvcloseport)中端口监视服务器 DLL 调用的函数。

有关这些操作的详细信息，请参阅的说明[ **ConfigurePortUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-configureportui)。 另请参阅[存储端口的配置信息](storing-port-configuration-information.md)。

 

 




