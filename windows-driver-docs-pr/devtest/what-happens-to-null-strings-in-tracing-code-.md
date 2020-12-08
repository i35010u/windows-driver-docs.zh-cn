---
title: 跟踪代码中的 NULL 字符串会发生什么情况
description: 跟踪代码中的 NULL 字符串会发生什么情况
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e11dddd244256aec4b3a4b3d3067faf109e437f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810715"
---
# <a name="what-happens-to-null-strings-in-tracing-code"></a>跟踪代码中的 NULL 字符串会发生什么情况？


默认情况下，此版本 Windows 驱动程序工具包中的跟踪组件 (WDK) 搜索在函数中传递的参数中的 **空** 字符串。 因此，不必验证每个参数以防止 **空** 字符串导致异常。

在 WDK 的早期版本中，对 \_ \_ \_ NULL \_ 字符串宏执行此函数的 WPP 检查。 如果使用此版本的 WDK 构建内核模式驱动程序或用户模式应用程序，则可以从源代码中删除宏。

 

 





