---
title: 初始化打印监视器
description: 初始化打印监视器
ms.assetid: 006727dd-aa0f-451c-b1c9-983d0c6401df
keywords:
- 打印监视器 WDK，初始化
- 初始化打印监视器
- LoadLibrary
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c714680104f6f97518b200f62281c851d6a6db3
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89205891"
---
# <a name="initializing-a-print-monitor"></a>初始化打印监视器





当后台处理程序调用 LoadLibrary 加载打印监视器 DLL 时，系统会立即调用 DLL 的 **DllEntryPoint** 函数。 通常情况下，入口点函数调用 DisableThreadLibraryCalls （如 Microsoft Windows SDK 文档中所述），这样就不会在创建和删除线程时不必要地通知 DLL。

每个 DLL 都导出一个初始化函数，在调用 LoadLibrary 后，后台处理程序将调用该函数。 语言监视器 Dll 和端口监视器服务器 Dll 导出 [**InitializePrintMonitor2**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintmonitor2) 函数。 端口监视器 UI Dll 导出 [**InitializePrintMonitorUI**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintmonitorui) 函数。

这两个初始化函数负责将指针返回到 [打印监视器定义](functions-defined-by-print-monitors.md)的其他函数，因此后台处理程序可以调用它们。 初始化函数还可以执行加载时初始化操作。 监视器的 [**InitializePrintMonitor2**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintmonitor2) 函数返回监视器实例句柄。 监视器应分配本地内存以存储特定于实例的信息，并使用监视句柄作为分配的内存的标识符。

当后台处理程序首次启动时，它会加载所有已安装的监视器 Dll。 在调用所有监视器初始化函数后，后台处理程序会调用每个端口监视器的 [**EnumPorts**](/previous-versions/ff548754(v=vs.85)) 函数，该函数枚举监视器支持的端口。 如果端口已添加到监视器数据库， (监视器支持端口，如 [添加端口](adding-a-port.md)中所述 ) 。随后将打开每个受支持的端口，如 [打开和关闭端口](opening-and-closing-a-port.md)中所述。

 

