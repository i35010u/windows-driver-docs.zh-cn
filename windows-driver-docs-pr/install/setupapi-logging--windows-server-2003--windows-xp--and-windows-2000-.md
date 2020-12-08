---
title: 'Setupapi.log 日志记录 (Windows Server 2003、Windows XP、Windows 2000) '
description: SetupAPI 日志记录（Windows Server 2003、Windows XP 和 Windows 2000）
keywords:
- Setupapi.log WDK 设备安装，日志记录
- 记录 WDK Setupapi.log
- Setupapi.log 日志记录 WDK Windows Server 2003
- Setupapi.log 日志记录 WDK Windows 2000
- Setupapi.log 日志记录 WDK Windows XP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 633a4d2b1d0680fb1bf2e4052c214f2876fb115b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838903"
---
# <a name="setupapi-logging-windows-server-2003-windows-xp-and-windows-2000"></a>SetupAPI 日志记录（Windows Server 2003、Windows XP 和 Windows 2000）





Windows 安装程序和设备安装程序服务（也称为 Setupapi.log）包含用于控制安装和设备安装的 Windows 功能。 安装程序继续时， [常规安装函数](/previous-versions/ff544985(v=vs.85)) (**安装程序**_xxx_ 函数) 和 [设备安装功能](/previous-versions/ff541299(v=vs.85)) (**SetupDi**_xxx_ 函数) 创建一个日志文件，用于提供用于解决设备安装问题的有用信息。

Setupapi.log 将日志记录到文件%*systemroot* % \\ *setupapi.log* 中。 日志文件是一个纯文本文件。 若要重置日志，请重命名或删除该文件。

本部分包含以下信息：

[设置 SetupAPI 日志记录级别](setting-setupapi-logging-levels.md)

[解释示例 SetupAPI 日志文件](interpreting-a-sample-setupapi-log-file.md)

 

