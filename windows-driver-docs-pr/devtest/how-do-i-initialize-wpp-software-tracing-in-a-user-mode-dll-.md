---
title: 如何初始化 WPP 软件跟踪在用户模式 DLL 中
description: 如何初始化 WPP 软件跟踪在用户模式 DLL 中
ms.assetid: 386ed1ba-8a6e-469d-9a03-c8879efd2613
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14d05ffa0b00b0d9d729ba44873347aae7bece58
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329930"
---
# <a name="how-do-i-initialize-wpp-software-tracing-in-a-user-mode-dll"></a>如何在用户模式 DLL 中初始化 WPP 软件跟踪？


从 Windows XP，您可以通过调用初始化 WPP 跟踪在用户模式 DLL [WPP\_INIT\_跟踪](https://msdn.microsoft.com/library/windows/hardware/ff556191)宏来初始化 WPP 软件跟踪。

若要避免错误，请使用以下方法。

-   调用[WPP\_INIT\_跟踪](https://msdn.microsoft.com/library/windows/hardware/ff556191)中的宏[DllMain](https://go.microsoft.com/fwlink/p/?linkid=179361)函数的 dll。

-   如果您的 DLL 用 C 编写的将添加 **\#定义** 语句 **WPP\_OLDCC**到你的源代码。 将之前定义放 **\#包括**语句[跟踪消息标头 (.tmh) 文件](trace-message-header-file.md)。 **WPP\_OLDCC**定义为仅为 C 代码。 不需要C++。

    例如：

    ```
    #define WPP_OLDCC
    #include "init.tmh"
    ```

无法初始化中的 WPP 软件跟踪**DllMain** Microsoft Windows 2000 上的函数。 由于 WPP 作为服务的一部分在上运行 Windows 2000，初始化软件跟踪生成 DLL 初始化期间禁止的远程过程调用。

 

 





