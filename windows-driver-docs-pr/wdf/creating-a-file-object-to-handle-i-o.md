---
title: 创建文件对象来处理 I/O
description: 创建文件对象来处理 I/O
ms.assetid: 3cd826fc-5c67-4ab4-800a-b5aa4bd5244f
keywords:
- 文件对象来处理 I/O WDK UMDF
- 文件对象来处理 I/O WDK UMDF，创建
- I/O 请求 WDK UMDF，文件对象
- 用户模式驱动程序框架 WDK，I/O 句柄的文件对象
- UMDF WDK，I/O 句柄的文件对象
- 用户模式驱动程序 WDK UMDF 文件 I/O 句柄的对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e69304899e9498edf06adbdac93092d7d5a4e856
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358504"
---
# <a name="creating-a-file-object-to-handle-io"></a>创建文件对象来处理 I/O

[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

当应用程序打开文件句柄时，I/O 管理器创建的文件对象。 Framework 又创建框架文件对象来表示 I/O 管理器的文件对象。

除非驱动程序设置**UmdfFileObjectPolicy**指令**AllowNullAndUnknownFileObjects**，UMDF 需要与文件对象相关联的每个 I/O 请求。 有关此指令的详细信息，请参阅[INF 文件中指定 WDF 指令](specifying-wdf-directives-in-inf-files.md)。

如果 UMDF 驱动程序发送 I/O 无关的应用程序到堆栈中的下一步驱动程序 （例如，在设备初始化期间或获取设备事件的通知），该驱动程序必须创建其自己的文件对象来将与请求相关联。

以下部分介绍驱动程序创建文件对象和应用程序创建文件对象和驱动程序如何创建和使用的文件对象之间的差异。

-   [创建驱动程序与应用程序创建文件对象](driver-created-versus-application-created-file-objects.md)
-   [创建和使用驱动程序创建文件对象](creating-and-using-driver-created-file-objects.md)

 

 





