---
title: 创建文件对象来处理 I/O
description: 创建文件对象来处理 I/O
ms.assetid: 3cd826fc-5c67-4ab4-800a-b5aa4bd5244f
keywords:
- 用于处理 i/o WDK UMDF 的文件对象
- 用于处理 i/o WDK UMDF 的文件对象，创建
- I/o 请求 WDK UMDF，file 对象
- 用户模式驱动程序框架 WDK，处理 i/o 的文件对象
- UMDF WDK，处理 i/o 的文件对象
- 用户模式驱动程序 WDK UMDF，处理 i/o 的文件对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d60970accb3c12d1cca183e03e502d5efab20a39
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210225"
---
# <a name="creating-a-file-object-to-handle-io"></a>创建文件对象来处理 I/O

[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

当应用程序打开文件句柄时，i/o 管理器将创建文件对象。 然后，框架会创建一个框架文件对象来表示 i/o 管理器的文件对象。

除非驱动程序将**UmdfFileObjectPolicy**指令设置为**AllowNullAndUnknownFileObjects**，否则，UMDF 要求每个 i/o 请求都与一个文件对象相关联。 有关此指令的详细信息，请参阅[在 INF 文件中指定 WDF 指令](specifying-wdf-directives-in-inf-files.md)。

如果 UMDF 驱动程序将独立于应用程序的 i/o 发送到堆栈中的下一个驱动程序（例如，在设备初始化期间或获取设备事件的通知），则驱动程序必须创建其自己的文件对象以与请求相关联。

以下各节描述了驱动程序创建的文件对象和应用程序创建的文件对象之间的差异，以及驱动程序创建和使用文件对象的方式。

-   [驱动程序创建的文件对象与应用程序创建的文件对象](driver-created-versus-application-created-file-objects.md)
-   [创建和使用驱动程序创建的文件对象](creating-and-using-driver-created-file-objects.md)

 

 





