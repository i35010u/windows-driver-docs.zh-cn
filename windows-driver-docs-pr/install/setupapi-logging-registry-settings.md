---
title: SetupAPI 日志记录注册表设置
description: SetupAPI 日志记录注册表设置
keywords:
- Setupapi.log 日志记录 WDK Windows Vista，注册表设置
- 注册表 WDK Setupapi.log 日志记录
- 事件级别 WDK Setupapi.log 日志记录
- 事件类别 WDK Setupapi.log 日志记录
- 文本日志 WDK Setupapi.log，注册表项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80f63e9fe514e5f27a1fcf8b5e322e16fb3a30f9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838895"
---
# <a name="setupapi-logging-registry-settings"></a>SetupAPI 日志记录注册表设置


[Setupapi.log](setupapi.md) 日志记录支持全局 *事件级别* 和全局 *事件类别* ，该类别控制是否将信息写入文本日志。 事件级别控制写入文本日志的详细信息级别，事件类别确定可生成日志项的操作的类型。 如果日志条目的事件级别为小于或等于文本日志的全局事件级别，并且为文本日志启用了日志条目的事件类别，则会将日志条目写入文本日志;否则，日志条目不会写入到文本日志中。

有关如何设置事件级别的信息，请参阅 [设置文本日志的事件级别](setting-the-event-level-for-a-text-log.md)。

有关如何为日志启用事件类别的信息，请参阅 [启用文本日志的事件类别](enabling-event-categories-for-a-text-log.md)。

默认情况下，setupapi.log 文本日志位于%*SystemRoot* % *\\ Inf* 目录中。 有关如何更改文本日志所在的目录的信息，请参阅 [设置文本日志的目录路径](setting-the-directory-path-of-the-text-logs.md)。

 

 





