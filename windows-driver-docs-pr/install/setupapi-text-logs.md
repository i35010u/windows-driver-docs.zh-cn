---
title: SetupAPI 文本日志
description: SetupAPI 文本日志
keywords:
- 文本日志 WDK Setupapi.log
- 设备安装文本记录 WDK
- 应用程序安装文本日志 WDK
- 日志条目 WDK Setupapi.log
- 文本日志标头 WDK Setupapi.log
- 文本日志节 WDK Setupapi.log
- Setupapi.log 日志记录 WDK Windows Vista，文本日志
- 文本日志 WDK Setupapi.log，关于文本日志
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31f18947995ba14fd038e03bf9601a45e8d423ff
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838897"
---
# <a name="setupapi-text-logs"></a>SetupAPI 文本日志


在 Windows Vista 和更高版本的 Windows 中， [setupapi.log](setupapi.md) 支持设备安装文本日志 (*setupapi.log*) 和应用程序安装文本日志 (*setupapi.log*) 。 即插即用 (PnP) manager 和 Setupapi.log 向设备安装文本日志写入条目，以提供有关安装设备和驱动程序的操作的信息。 PnP 管理器和 Setupapi.log 将条目写入到应用程序安装文本日志，该日志提供有关特定于设备和驱动程序安装的特定于安装操作的信息。

安装应用程序、类安装程序和共同安装程序可以使用 [setupapi.log 日志记录功能](using-the-setupapi-logging-functions.md) 将条目写入设备安装日志和应用程序安装文本日志中。

Setupapi.log 文本日志是 ANSI 纯文本文件，默认情况下位于 *% SystemRoot% \\ inf* 目录中。 文本日志采用英语 (标准) 语言。

Setupapi.log 文本日志具有以下内部格式：

-   *日志条目* 在文本日志中占一行。

-   前几个日志条目提供 *文本日志标头* ，其中包含有关操作系统和计算机体系结构的信息。 有关详细信息，请参阅 [文本日志标头的格式](format-of-a-text-log-header.md)。

-   文本日志标头之后为零个或多个 *文本日志部分*。 每个文本日志部分记录单个设备安装过程中的事件。

    文本日志部分的目的是对提供有关特定安装操作的信息的一系列连续日志条目进行分组和格式化。 通过创建文本日志节，PnP 管理器、Setupapi.log 或自定义安装应用程序可以通过概念上有意义的方式来组织日志条目。 例如，PnP 管理器可能会创建一个文本日志部分，以对应用于安装设备的所有日志条目进行分组。 文本日志节按创建顺序出现在文本日志中。 有关详细信息，请参阅 [文本日志的格式部分](format-of-a-text-log-section.md)。

-   文本日志可以包含不属于文本日志标头或文本日志部分的日志项。 此类项与不属于任何特定文本日志部分的操作相关联，并且通常会在文本日志节之间交错。 不属于文本日志部分的日志条目将按照它们写入文本日志的相同顺序出现在日志中。 有关此类日志条目的详细信息，请参阅 [不属于文本日志的日志条目的格式部分](format-of-log-entries-that-are-not-part-of-a-text-log-section.md)。

 

 





