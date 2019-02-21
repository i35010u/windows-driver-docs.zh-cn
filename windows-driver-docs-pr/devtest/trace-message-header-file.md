---
title: 跟踪消息标头文件
description: 跟踪消息标头文件
ms.assetid: 835162c0-6596-42ae-bc6d-824dd6c3f69f
keywords:
- 跟踪消息标头文件 WDK
- TMH 文件 WDK
- 文件 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49a75ba013366393766b8f91866a30fb974fb37e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544359"
---
# <a name="trace-message-header-file"></a>跟踪消息标头文件


一个*跟踪消息标头*(TMH) 文件是包含声明的函数和变量使用 WPP 生成的跟踪代码的文本文件。 标头文件还包括添加跟踪消息格式到 PDB 文件的说明的宏[跟踪提供程序](trace-provider.md)，如内核模式驱动程序或用户模式应用程序。

WPP TMH 文件会自动生成编译时[跟踪提供程序](trace-provider.md)包括 WPP 宏。 TMH 文件作为源文件，但扩展名为.tmh 具有相同的名称。 WPP 将文件保存在与源文件相同的目录中。

当将 WPP 宏添加到源代码时，还必须添加**\#包括**指令将生成 WPP TMH 文件。 Include 语句采用以下格式：

```
#include SourceFileName.tmh
```

这包括语句后的定义必须出现[WPP\_控制\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff556186)宏，但对 WPP 宏的任何调用之前。

有关详细信息，请参阅[添加到跟踪制造者 WPP 宏](adding-wpp-macros-to-a-trace-provider.md)，并查看[TraceDrv](https://go.microsoft.com/fwlink/p/?LinkId=617726)，为软件跟踪设计的一个示例驱动程序。 TraceDrv 示例现已推出[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub 上的存储库。

 

 





