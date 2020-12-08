---
title: BindPrinter
description: IPrintTicketProvider BindPrinter 方法将打印机或打印队列绑定到打印票证架构的特定版本。
keywords:
- BindPrinter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c463cbd87e8746d17da9ff73f110c54aeadf7616
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797783"
---
# <a name="bindprinter"></a>BindPrinter


[**IPrintTicketProvider：： BindPrinter**](/previous-versions/windows/hardware/drivers/ff554354(v=vs.85))方法将打印机或打印队列绑定到打印票证架构的特定版本。 这使得核心驱动程序可以将一组专用命名空间 Uri 与设备相关联。

绑定到设备后，提供程序可以缓存某些对象和句柄，该对象和句柄会用于为该设备执行将来的打印票证或设备功能服务。

对于每个 PrintTicketProvider 实例，都保证只调用一次 [**IPrintTicketProvider：： BindPrinter**](/previous-versions/windows/hardware/drivers/ff554354(v=vs.85)) 方法。

下面的示例代码演示了方法的参数。

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
