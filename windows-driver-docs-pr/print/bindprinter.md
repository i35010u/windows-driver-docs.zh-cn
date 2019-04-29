---
title: BindPrinter
description: IPrintTicketProvider BindPrinter 方法绑定到特定版本的打印票证架构打印机或打印队列。
ms.assetid: 81f32a9a-417a-4851-972e-373112590e1c
keywords:
- BindPrinter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b6fcc1d89295dc760f0e9fd41795e83f8e0bebc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390617"
---
# <a name="bindprinter"></a>BindPrinter


[ **IPrintTicketProvider::BindPrinter** ](https://msdn.microsoft.com/library/windows/hardware/ff554354)方法将打印机或打印队列绑定到特定版本的打印票证架构。 这使核心驱动程序将一组专用命名空间 Uri 与设备相关联。

绑定到的设备启用的提供程序缓存某些对象和处理，它将用于执行未来打印票证或设备功能服务，该设备。

[ **IPrintTicketProvider::BindPrinter** ](https://msdn.microsoft.com/library/windows/hardware/ff554354)方法保证将为每个 PrintTicketProvider 实例一次调用。

下面的示例代码说明了该方法的参数。

```cpp
STDMETHODIMP 
CPrintTicketProvider::
BindPrinter( THIS_ HANDLE    hPrinter,
                   INT       version,
                   PSHIMOPTS pOptions,
                   DWORD    *pDevModeFlags,
                   INT      *pcNamespaces,
                   BSTR    **ppNamespaces)
```
