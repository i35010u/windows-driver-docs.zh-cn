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
ms.openlocfilehash: e54ede885448afa733d60386a4b5efb12b40f06b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385988"
---
# <a name="initializing-a-print-monitor"></a>初始化打印监视器





当后台处理程序调用 LoadLibrary 加载 DLL 的打印监视器时，系统会立即调用的 DLL **DllEntryPoint**函数。 它通常是个好主意入口点函数调用 DisableThreadLibraryCalls，因此 DLL 时创建和删除线程不会不必要地通知 Microsoft Windows SDK 文档中所述。

每个 DLL 导出后台处理程序调用 LoadLibrary 后调用的初始化函数。 语言监视 Dll 和端口监视器服务器 Dll 导出[ **InitializePrintMonitor2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-initializeprintmonitor2)函数。 端口监视器 UI Dll 导出[ **InitializePrintMonitorUI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-initializeprintmonitorui)函数。

这两个初始化函数负责返回指向函数的其余部分[函数定义的打印监视器](functions-defined-by-print-monitors.md)，因此后台处理程序可以调用它们。 初始化函数还可以执行加载时初始化操作。 监视器[ **InitializePrintMonitor2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-initializeprintmonitor2)函数将返回一个监视器实例句柄。 监视器应分配本地内存来存储特定于实例的信息，并使用监视器句柄作为标识符已分配的内存。

当首次启动后台处理程序时，它会加载所有监视器已安装的 Dll。 调用后所有监视器初始化函数，后台处理程序调用每个端口监视器[ **EnumPorts** ](https://docs.microsoft.com/previous-versions/ff548754(v=vs.85))函数，可枚举受监视的端口。 (Monitor 支持端口如果端口已添加到监视器的数据库，如中所述[添加一个端口](adding-a-port.md)。)每个受支持，然后打开端口，如中所述[打开和关闭端口](opening-and-closing-a-port.md)。

 

 




