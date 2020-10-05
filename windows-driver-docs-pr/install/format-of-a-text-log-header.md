---
title: 文本日志标头的格式
description: 文本日志标头的格式
ms.assetid: d4a50905-215f-4156-b5cf-f160c757bb90
keywords:
- 标头 WDK Setupapi.log 日志记录
- 格式化 WDK Setupapi.log 日志记录
- 文本日志 WDK Setupapi.log、标头
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ec45980fa3e1a8bec6feffc2f3c24d617c5fb3a
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733951"
---
# <a name="format-of-a-text-log-header"></a>文本日志标头的格式


*文本日志标头*由 setupapi.log 文本日志中的前几个日志项组成。 Text 日志标头包含有关操作系统和系统体系结构的信息。 下面是文本日志标头的一个示例：

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

 

