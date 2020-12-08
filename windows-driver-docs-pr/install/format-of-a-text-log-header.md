---
title: 文本日志标头的格式
description: 文本日志标头的格式
keywords:
- 标头 WDK Setupapi.log 日志记录
- 格式化 WDK Setupapi.log 日志记录
- 文本日志 WDK Setupapi.log、标头
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4964e56603a8461386650753c24b2ff592ae08ef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820189"
---
# <a name="format-of-a-text-log-header"></a>文本日志标头的格式


*文本日志标头* 由 setupapi.log 文本日志中的前几个日志项组成。 Text 日志标头包含有关操作系统和系统体系结构的信息。 下面是文本日志标头的一个示例：

```cpp
[Device Install Log]
     OS Version = 6.0.5033
     Service Pack = 0.0
     Suite = 0x0100
     ProductType = 1
     Architecture = x86

[BeginLog]
```

文本日志标头中的信息是通过调用[OVSERVERSIONINFOEX](/windows/win32/api/winnt/ns-winnt-osversioninfoexa)结构中的[GetVersionEx](/windows/win32/api/sysinfoapi/nf-sysinfoapi-getversionexa)返回的信息的子集。 有关详细信息，请参阅 Microsoft Windows SDK。

 

