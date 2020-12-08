---
title: 添加端口
description: 添加端口
keywords:
- 端口管理 WDK 打印，添加端口
- 添加端口
- AddPort
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c3db05dd0dff10bb3b57caba01a011f4b6bc66e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812417"
---
# <a name="adding-a-port"></a>添加端口





添加端口包括将端口名称和用户可修改的配置信息存储在端口监视器服务器 DLL 的本地存储或注册表中。

当应用程序调用打印后台处理程序的 AddPort 函数时 (Microsoft Windows SDK 文档) 中所述，它将端口监视器的名称指定为函数自变量。 后台处理程序将调用指定端口监视器的端口监视器 UI DLL 中包含的 [**AddPortUI**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-addportui) 函数。

端口监视器 UI DLL 的 [**AddPortUI**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-addportui) 函数应执行以下操作：

1.  调用打印后台处理程序的 OpenPrinter 函数 (Windows SDK 文档) 中所述，这将导致调用端口监视器服务器 DLL 中的 [**XcvOpenPort**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvopenport) 函数。

2.  多次调用打印后台处理程序的 [**XcvData**](/previous-versions/ff564255(v=vs.85)) 函数，以请求端口监视器服务器 DLL 添加端口并在 UI dll 和服务器 dll 之间传输配置信息。 **XcvData** 函数调用服务器 DLL 的 [**XcvDataPort**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvdataport)函数。 [**AddPortUI**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-addportui)函数通常通过显示对话框从用户那里获取配置信息。

3.  调用打印后台处理程序的 ClosePrinter 函数 (Windows SDK 文档) 中所述，这将导致调用端口监视器服务器 DLL 中的 [**XcvClosePort**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvcloseport) 函数。

有关这些操作的详细信息，请参阅 [**AddPortUI**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-addportui)的说明。 另请参阅 [存储端口配置信息](storing-port-configuration-information.md)。

端口监视器的 [**EnumPorts**](/previous-versions/ff548754(v=vs.85)) 函数必须枚举已添加的所有端口。 后台处理程序可以调用每个端口监视器的 **EnumPorts** 函数来确定打印服务器上支持的端口集。

 

