---
title: 配置端口
description: 配置端口
ms.assetid: f5996e94-aa48-4aa0-82f5-331a57d2fb6b
keywords:
- 端口管理 WDK 打印，配置端口
- ConfigurePort
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da49c0aa9b7342d208c6526c88524ee4ddf73719
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214949"
---
# <a name="configuring-a-port"></a>配置端口





配置端口包括为先前添加的端口修改端口监视器服务器 DLL 的存储配置信息。

当应用程序调用打印后台处理程序的 [**ConfigurePort**](/previous-versions/ff546286(v=vs.85)) 函数时 (Microsoft Windows SDK 文档) 中所述， **ConfigurePort** 函数会调用相应端口监视器的端口监视器 UI DLL 中包含的 [**ConfigurePortUI**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-configureportui) 函数。

端口监视器 UI DLL 的 [**ConfigurePortUI**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-configureportui) 函数应执行以下操作：

1.  调用打印后台处理程序的 OpenPrinter 函数 (Windows SDK 文档) 中所述，这将导致调用端口监视器服务器 DLL 中的 [**XcvOpenPort**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvopenport) 函数。

2.  一次或多次调用打印后台处理程序的 [**XcvData**](/previous-versions/ff564255(v=vs.85)) 函数，以便在 UI dll 和服务器 dll 之间传输配置信息。 **XcvData**函数调用服务器 DLL 的[**XcvDataPort**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvdataport)函数。 [**ConfigurePortUI**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-configureportui)函数通常通过显示对话框从用户那里获取配置信息。

3.  调用打印后台处理程序的 ClosePrinter 函数 (Windows SDK 文档) 中所述，这将导致调用端口监视器服务器 DLL 中的 [**XcvClosePort**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvcloseport) 函数。

有关这些操作的详细信息，请参阅 [**ConfigurePortUI**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-configureportui)的说明。 另请参阅 [存储端口配置信息](storing-port-configuration-information.md)。

 

