---
title: 跟踪消息标头文件
description: 跟踪消息标头文件
ms.assetid: 835162c0-6596-42ae-bc6d-824dd6c3f69f
keywords:
- 跟踪消息头文件 WDK
- TMH 文件 WDK
- 文件 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0842b909cf07b4862ba4ffca349cd8fbef5579b1
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382777"
---
# <a name="trace-message-header-file"></a>跟踪消息标头文件


*跟踪消息标头* (TMH) 文件是一个文本文件，该文件包含 WPP 生成的跟踪代码所使用的函数和变量的声明。 标头文件还包括将跟踪消息格式设置指令添加到 [跟踪提供程序](trace-provider.md)的 PDB 文件（如内核模式驱动程序或用户模式应用程序）的宏。

当你编译包含 WPP 宏的 [跟踪提供程序](trace-provider.md) 时，WPP 会自动生成 TMH 文件。 TMH 文件具有与源文件相同的名称，但文件扩展名为 TMH。 WPP 将该文件保存在源文件所在的同一目录中。

向源代码添加 WPP 宏时，还必须为 WPP 将生成的 TMH 文件添加** \# 包含**指令。 Include 语句的形式为：

```
#include SourceFileName.tmh
```

此 include 语句必须出现在 [wpp \_ 控件 \_ guid](/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85)) 宏的定义之后、在对 wpp 宏的任何调用之前。

有关详细信息，请参阅 [向跟踪生成程序添加 WPP 宏](adding-wpp-macros-to-a-trace-provider.md) 和查看 [TraceDrv](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/tracing/tracedriver)（一个用于软件跟踪的示例驱动程序）。 GitHub 上的 [Windows 驱动程序示例](https://github.com/Microsoft/Windows-driver-samples) 存储库中提供了 TraceDrv 示例。

 

