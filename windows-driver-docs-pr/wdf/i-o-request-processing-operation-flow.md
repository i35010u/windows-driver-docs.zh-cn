---
title: I/O 请求处理操作流
description: I/O 请求处理操作流
keywords:
- 操作流 WDK UMDF
- I/o 请求 WDK UMDF，操作流
- 请求处理 WDK UMDF，操作流
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67b8c7bdfb8f59ee390be1cdb95d4836e09a613e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814713"
---
# <a name="io-request-processing-operation-flow"></a>I/O 请求处理操作流


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

所有 i/o 操作都发生在文件对象的上下文中 (也就是说，应用程序对 Microsoft Win32 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea) 和 **CloseHandle** 函数所做的调用之间将发生所有的 i/o 操作) 。 I/o 操作是应用程序所做的调用，例如 Win32 **ReadFileEx**、 **WriteFileEx** 和 [**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) 函数。

以下主题显示的是在单设备堆栈和双设备堆栈中，在 UMDF 驱动程序中和从 UMDF 驱动程序开始、处理和结束的操作流：

-   [使用单设备堆栈的操作流](operation-flow-with-single-device-stack.md)

-   [使用双设备堆栈的操作流](operation-flow-with-double-device-stack.md)

**注意**   应用程序启动的所有 i/o 都是通过内核模式路由的，如 UMDF 部分的 [体系结构](/previous-versions/ff554461(v=vs.85)) 中所示，即使 I/o 请求处理操作流部分中的数字未显示这种情况。

 

 

