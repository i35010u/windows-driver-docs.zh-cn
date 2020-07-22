---
title: 调试代码概述
description: 调试代码概述
ms.assetid: 2c76e569-61cd-44b0-b8e5-032ab2c48fdb
keywords:
- 调试驱动程序 WDK，调试代码
- 调试代码 WDK
- 调试代码 WDK，关于调试代码
ms.date: 07/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: f866194ba98dd08b40cde834a1b21fa00f62b9c4
ms.sourcegitcommit: 3ec971f54122b77408433f7f1e59c467099fb4de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86873834"
---
# <a name="debugging-code-overview"></a>调试代码概述

对于用户模式和内核模式驱动程序，可以使用特殊的调试例程、宏和全局变量。 通过在驱动程序代码中使用这些例程，你可以将消息发送到调试器并设置断点以帮助调试。

[条件编译和生成环境](conditional-compilation-and-the-build-environment.md)

有关调试的详细信息，请参阅文档中的以下主题：

[突入调试器](..\debugger\breaking-into-the-debugger.md)

[将输出发送到调试器](..\debugger\sending-output-to-the-debugger.md)

[读取和筛选调试消息](..\debugger\reading-and-filtering-debugging-messages.md)

[确定是否已附加调试器](..\debugger\determining-if-a-debugger-is-attached.md)
