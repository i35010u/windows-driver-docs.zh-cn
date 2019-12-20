---
title: I/O 请求处理操作流
description: I/O 请求处理操作流
ms.assetid: 3a7162d2-0a8c-4748-b320-bfe64ec93c9d
keywords:
- 操作流 WDK UMDF
- I/o 请求 WDK UMDF，操作流
- 请求处理 WDK UMDF，操作流
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6bc896e4aa505a703345e375290d461bac2b349
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209893"
---
# <a name="io-request-processing-operation-flow"></a>I/O 请求处理操作流


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

所有 i/o 操作都在文件对象的上下文中发生（也就是说，应用程序对 Microsoft Win32 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)和**CloseHandle**函数进行的调用之间发生所有 i/o 操作）。 I/o 操作是应用程序所做的调用，例如 Win32 **ReadFileEx**、 **WriteFileEx**和[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)函数。

以下主题显示的是在单设备堆栈和双设备堆栈中，在 UMDF 驱动程序中和从 UMDF 驱动程序开始、处理和结束的操作流：

-   [单个设备堆栈的操作流](operation-flow-with-single-device-stack.md)

-   [双设备堆栈的操作流](operation-flow-with-double-device-stack.md)

**请注意**  ，由应用程序启动的所有 i/o 都通过内核模式路由，如 UMDF 部分的[体系结构](https://docs.microsoft.com/previous-versions/ff554461(v=vs.85))中所示，即使 I/o 请求处理操作流部分中的数字未显示这种情况。

 

 

 





