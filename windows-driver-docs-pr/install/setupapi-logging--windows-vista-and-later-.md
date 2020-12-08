---
title: SetupAPI 日志记录
description: SetupAPI 日志记录
keywords:
- Setupapi.log WDK，日志记录
- 记录 WDK Setupapi.log
- Setupapi.log 日志记录 WDK Windows Vista
- Setupapi.log 日志记录 WDK Windows Vista，关于 Setupapi.log 日志记录
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e674df868fa554000ce638f2ff79a53ae9f8d958
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838901"
---
# <a name="setupapi-logging"></a>SetupAPI 日志记录


在 Windows Vista 和更高版本的 Windows 中， [setupapi.log](setupapi.md) 包括以下日志记录组件：

-   即插即用 (PnP) manager 和 Setupapi.log 日志信息，有关设备安装文本日志中的安装事件 (*setupapi.log*) 和应用程序安装文本日志 (*setupapi.log*) 。 设备安装文本日志包含有关设备和驱动程序安装的信息，应用程序安装文本日志包含有关与设备驱动程序安装相关联的应用程序软件安装的信息。 有关 Setupapi.log 文本日志内容的详细信息，请参阅 [Setupapi.log 文本日志](setupapi-text-logs.md); 有关如何启用日志记录的信息，请参阅 [Setupapi.log 日志记录注册表设置](setupapi-logging-registry-settings.md)。

-   [Setupapi.log 日志记录函数](/previous-versions/ff550878(v=vs.85))（PnP 设备安装应用程序、类安装程序和共同安装程序）可用于将日志条目写入 setupapi.log 文本日志。 有关如何使用这些函数的信息，请参阅 [使用 Setupapi.log 日志记录函数](using-the-setupapi-logging-functions.md)。

 

