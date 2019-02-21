---
title: SetupAPI 文本日志
description: SetupAPI 文本日志
ms.assetid: db2460f3-b716-4687-9b07-2047f74332d8
keywords:
- 文本日志 WDK SetupAPI
- 设备安装文本日志 WDK
- 应用程序安装文本日志 WDK
- 日志条目 WDK SetupAPI
- 文本日志文件头 WDK SetupAPI
- 文本日志部分 WDK SetupAPI
- SetupAPI 日志记录 WDK Windows Vista 中，文本日志
- 文本日志 WDK SetupAPI 关于文本日志
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 586814d72f73e69c0ecccff17677b11750020ef7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548232"
---
# <a name="setupapi-text-logs"></a>SetupAPI 文本日志


在 Windows Vista 和更高版本的 Windows， [SetupAPI](setupapi.md)支持的设备安装文本日志 (*SetupAPI.dev.log*) 和应用程序安装文本日志 (*SetupAPI.app.log*). 插即用 (PnP) 管理器和 SetupAPI 向日志写入条目设备安装文本以提供有关安装设备和驱动程序的操作的信息。 PnP 管理器和 SetupAPI 将项写入应用程序安装文本日志，提供有关安装操作，而非特定于设备和驱动程序安装相关的信息。

安装应用程序、 类的安装程序，以及共同安装程序可以使用[SetupAPI 日志记录功能](using-the-setupapi-logging-functions.md)向设备安装日志和应用程序安装文本日志写入条目。

SetupAPI 文本日志是 ANSI 纯文本格式文件，默认情况下位于 *%systemroot%\\inf*目录。 文本日志是以英语 (Standard)。

SetupAPI 文本日志具有以下内部格式：

-   一个*日志条目*是文本日志中的一行。

-   几个日志条目提供的第一个*文本日志标头*，包含有关操作系统和计算机体系结构信息。 有关详细信息，请参阅[文本日志标头的格式](format-of-a-text-log-header.md)。

-   以下文本日志标头是零个或多个*的文本日志部分*。 每个文本日志部分在单个设备安装过程中记录事件。

    文本日志部分的目的是组和格式提供特定的安装操作的相关信息的日志条目的连续序列。 通过创建文本日志部分，即插即用管理器、 安装程序 Api 或自定义安装应用程序可以从概念上讲有意义的方式组织日志条目。 例如，即插即用管理器可能创建了文本日志部分，让组适用于安装设备的所有日志条目。 在创建它们的顺序文本日志中出现的文本日志部分。 有关详细信息，请参阅[格式的文本日志部分](format-of-a-text-log-section.md)。

-   文本日志可以包含不是文本日志标头或文本日志部分的一部分的日志条目。 此类条目相关联，但不属于任何特定的文本日志部分，并在一般情况下，交错文本日志的各部分之间的操作。 不是文本日志部分的一部分的日志条目出现在日志中与文本日志写入相同的顺序。 有关此类详细信息日志条目，请参阅[格式的日志条目，是不属于文本日志部分](format-of-log-entries-that-are-not-part-of-a-text-log-section.md)。

 

 





