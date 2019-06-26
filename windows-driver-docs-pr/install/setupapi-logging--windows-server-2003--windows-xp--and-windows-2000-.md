---
title: SetupAPI 日志记录 (Windows Server 2003，Windows XP、 Windows 2000)
description: SetupAPI 日志记录（Windows Server 2003、Windows XP 和 Windows 2000）
ms.assetid: 5b35fad3-09d6-4b2f-9831-661fe69f2f99
keywords:
- SetupAPI WDK 设备安装，日志记录
- WDK SetupAPI 日志记录
- SetupAPI 日志记录 WDK Windows Server 2003
- SetupAPI 日志记录 WDK Windows 2000
- SetupAPI 日志记录 WDK Windows XP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb86ae995c82a828b8342079764b838d89c06164
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386393"
---
# <a name="setupapi-logging-windows-server-2003-windows-xp-and-windows-2000"></a>SetupAPI 日志记录（Windows Server 2003、Windows XP 和 Windows 2000）





Windows 安装程序和设备安装程序服务，也称为安装程序 Api，包括控制设置和设备安装的 Windows 函数。 安装程序继续进行，[常规安装函数](https://docs.microsoft.com/previous-versions/ff544985(v=vs.85))( **安装 * * * Xxx*函数) 和[设备安装函数](https://docs.microsoft.com/previous-versions/ff541299(v=vs.85))(* * SetupDi * * * Xxx*函数) 创建一个日志文件，提供设备安装问题疑难解答的有用信息。

SetupAPI 日志文件 %*systemroot*%\\*setupapi.log*。 日志文件是一个纯文本文件。 若要重置日志，请重命名或删除该文件。

本部分包括以下信息：

[设置 SetupAPI 日志记录级别](setting-setupapi-logging-levels.md)

[解释示例 SetupAPI 日志文件](interpreting-a-sample-setupapi-log-file.md)

 

 





