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
ms.openlocfilehash: 79377468a59511c59a79c3069ea1a49974e21b15
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533473"
---
# <a name="io-request-processing-operation-flow"></a>I/O 请求处理操作流


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

文件对象的上下文中发生的所有 I/O 操作 (即，所有 I/O 操作都都出现到 Microsoft Win32 应用程序进行的调用之间[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)和**CloseHandle**函数)。 I/O 操作都是对做的调用应用程序，例如，Win32 **ReadFileEx**， **writefileex 只写入**，并[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)函数。

以下主题可显示的时间与 UMDF 驱动程序执行用户 I/O 事务开始时，进程，并结束和 double 设备堆栈中的单个设备堆栈操作的流：

-   [与单个设备堆栈操作流](operation-flow-with-single-device-stack.md)

-   [与 Double 设备堆栈操作流](operation-flow-with-double-device-stack.md)

**请注意**  启动的应用程序的所有 I/O 都经过内核模式下，图形中所示[体系结构的 UMDF](https://msdn.microsoft.com/library/windows/hardware/ff554461)部分，即使图形中 I/O 请求处理操作流部分不会显示这种情况。

 

 

 





