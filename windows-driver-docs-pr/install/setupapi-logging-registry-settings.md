---
title: SetupAPI 日志记录注册表设置
description: SetupAPI 日志记录注册表设置
ms.assetid: 24694bce-5941-479f-9e2d-f9c7577a4f6a
keywords:
- SetupAPI 日志记录 WDK Windows Vista 中，注册表设置
- 注册表 WDK SetupAPI 日志记录
- 事件级别 WDK SetupAPI 日志记录
- 事件类别 WDK SetupAPI 日志记录
- 文本日志 WDK SetupAPI，注册表项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9307a0b28bb4ed6b635e03ceabac500836299750
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566132"
---
# <a name="setupapi-logging-registry-settings"></a>SetupAPI 日志记录注册表设置


[SetupAPI](setupapi.md)日志记录支持全局*事件级别*和全局*事件类别*，以控制是否将信息写入到文本日志。 事件级别控制写入到文本日志的详细信息的级别和事件类别确定的操作，可以使日志条目的类型。 如果日志条目都具有一个事件级别按数字顺序小于或等于的全局事件级别的文本日志，并且文本日志启用了日志条目的事件类别，日志条目写入到该文本日志。否则，日志条目不会写入到文本日志中。

有关如何设置事件级别的信息，请参阅[事件级别设置为文本日志](setting-the-event-level-for-a-text-log.md)。

有关如何设置启用了日志的事件类别的信息，请参阅[启用文本日志的事件类别](enabling-event-categories-for-a-text-log.md)。

默认情况下，安装程序 Api 文本日志文件位于 %*SystemRoot*%*\\Inf*目录。 有关如何更改文本日志所在的目录的信息，请参阅[设置的文本日志目录路径](setting-the-directory-path-of-the-text-logs.md)。

 

 





