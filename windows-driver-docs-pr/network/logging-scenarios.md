---
title: 日志记录方案
description: 本主题介绍 IHV 跟踪 WDI 驱动程序中的日志记录的用户启动反馈的日志记录方案。
ms.assetid: B9E10527-9C25-46B6-ADC2-4CF5AB749E04
ms.date: 06/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5397717ab4f81be578f50c105f560db489d4a000
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340934"
---
# <a name="logging-scenarios"></a>日志记录方案

针对重现模式和自动记录器，IHV 日志文件中保存的事件应适当地通过标志/级别/关键字来确保至少 30 分钟的日志事件始终保存在过去受到限制。 实际上，应针对 30 分钟时间段内以涵盖一个扫描/WFD 发现，一个连接/漫游事件，其中一个断开连接事件、 多个 power 转换和 10 分钟的发送和接收数据。 由于 IHV 重现模式日志比正常 IHV 自动-记录器大得多，应更详细的记录。

以下方案可帮助您进行日志记录时：

- 获取连接
- 电源转换
- 单选管理
- Roaming
- Hang/recovery
- 从转换连接到受限

## <a name="related-links"></a>相关链接

[用户启动使用 IHV 跟踪日志记录的反馈](user-initiated-feedback-with-ihv-trace-logging.md)
