---
title: 日志记录方案
description: 本主题介绍在 WDI 驱动程序中通过 IHV 跟踪日志记录执行用户启动的反馈的日志记录方案。
ms.date: 06/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: b3557d25487c27c257f2e88a6b9852a7dda3b202
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833393"
---
# <a name="logging-scenarios"></a>日志记录方案

对于重现模式和自动记录器，保存在 IHV 日志文件中的事件应该通过标志/级别/关键字进行适当的限制，以确保至少保存最近30分钟的日志事件。 实际上，应将30分钟的时间段设定为涵盖一个扫描/WFD 发现、一个连接/漫游事件、一个断开事件、几个电源转换和10分钟的发送和接收数据。 由于 IHV 重现模式日志比普通 IHV 自动记录器要大得多，因此需要更详细的日志记录。

日志记录时，下列方案可能会有所帮助：

- 正在连接
- 电源转换
- 无线电管理
- 漫游
- 挂起/恢复
- 从连接到受限的转换

## <a name="related-links"></a>相关链接

[用户使用 IHV 跟踪日志记录发起的反馈](user-initiated-feedback-with-ihv-trace-logging.md)
