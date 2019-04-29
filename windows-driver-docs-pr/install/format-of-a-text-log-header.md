---
title: 文本日志标头的格式
description: 文本日志标头的格式
ms.assetid: d4a50905-215f-4156-b5cf-f160c757bb90
keywords:
- 标头 WDK SetupAPI 日志记录
- 格式 WDK SetupAPI 日志记录
- 文本日志 WDK SetupAPI，标头
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d25176111815715564f42650e9d74eb0cb485468
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377078"
---
# <a name="format-of-a-text-log-header"></a>文本日志标头的格式


一个*文本日志标头*包含 SetupAPI 文本日志中的第几个日志条目。 文本日志标头包含有关操作系统和系统体系结构的信息。 以下是文本日志标头的示例：

```cpp
[Device Install Log]
     OS Version = 6.0.5033
     Service Pack = 0.0
     Suite = 0x0100
     ProductType = 1
     Architecture = x86

[BeginLog]
```

文本日志标头中的信息是通过调用返回的信息的子集[GetVersionEx](https://go.microsoft.com/fwlink/p/?linkid=179601)中[OVSERVERSIONINFOEX](https://go.microsoft.com/fwlink/p/?linkid=179602)结构。 有关详细信息，请参阅 Microsoft Windows SDK。

 

 





