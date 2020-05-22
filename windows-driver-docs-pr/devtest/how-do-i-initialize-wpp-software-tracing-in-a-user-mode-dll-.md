---
title: 如何实现在用户模式 DLL 中初始化 WPP 软件跟踪
description: 如何实现在用户模式 DLL 中初始化 WPP 软件跟踪
ms.assetid: 386ed1ba-8a6e-469d-9a03-c8879efd2613
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fdda67c255e8e7c6fe0ff5e251546ddbb41a109
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769639"
---
# <a name="how-do-i-initialize-wpp-software-tracing-in-a-user-mode-dll"></a>如何在用户模式 DLL 中初始化 WPP 软件跟踪？


从 Windows XP 开始，可以通过调用[wpp \_ INIT \_ 跟踪](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))宏初始化 wpp 软件跟踪，在用户模式 DLL 中初始化 wpp 跟踪。

若要避免错误，请使用以下方法。

-   在 DLL 的[DllMain](https://docs.microsoft.com/windows/win32/dlls/dllmain)函数中调用[WPP \_ INIT \_ 跟踪](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))宏。

-   如果 DLL 是用 C 编写的，则将用于**WPP \_ OLDCC**的** \# define**语句添加到源代码中。 将定义放置在[跟踪消息头（. tmh）文件](trace-message-header-file.md)的** \# include**语句前面。 只有 C 代码需要**WPP \_ OLDCC**定义。 C + + 不需要此方法。

    例如：

    ```
    #define WPP_OLDCC
    #include "init.tmh"
    ```

无法在 Microsoft Windows 2000 上的**DllMain**函数中初始化 WPP 软件跟踪。 因为 WPP 作为 Windows 2000 上的服务的一部分运行，所以，初始化软件跟踪会生成一个远程过程调用，在 DLL 初始化期间禁止此操作。

 

 





