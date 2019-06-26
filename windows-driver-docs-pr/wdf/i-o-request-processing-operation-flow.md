---
title: I/O 请求处理操作流
description: I/O 请求处理操作流
ms.assetid: 3a7162d2-0a8c-4748-b320-bfe64ec93c9d
keywords:
- 操作流 WDK UMDF
- I/O 请求 WDK UMDF，操作流
- 请求处理 WDK UMDF，操作流
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80d7dfce927375098095d3db692bb67405203f93
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382826"
---
# <a name="io-request-processing-operation-flow"></a>I/O 请求处理操作流


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

文件对象的上下文中发生的所有 I/O 操作 (即，所有 I/O 操作都都出现到 Microsoft Win32 应用程序进行的调用之间[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)和**CloseHandle**函数)。 I/O 操作都是对做的调用应用程序，例如，Win32 **ReadFileEx**， **writefileex 只写入**，并[ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)函数。

以下主题可显示的时间与 UMDF 驱动程序执行用户 I/O 事务开始时，进程，并结束和 double 设备堆栈中的单个设备堆栈操作的流：

-   [与单个设备堆栈操作流](operation-flow-with-single-device-stack.md)

-   [与 Double 设备堆栈操作流](operation-flow-with-double-device-stack.md)

**请注意**  启动的应用程序的所有 I/O 都经过内核模式下，图形中所示[体系结构的 UMDF](https://docs.microsoft.com/previous-versions/ff554461(v=vs.85))部分，即使图形中 I/O 请求处理操作流部分不会显示这种情况。

 

 

 





