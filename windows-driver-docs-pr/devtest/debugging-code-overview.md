---
title: 调试代码概述
description: 调试代码概述
keywords:
- 调试驱动程序 WDK，调试代码
- 调试代码 WDK
- 调试代码 WDK，关于调试代码
ms.date: 07/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: 19bd08b8f6afd5669798473827cdacc02468cb35
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817841"
---
# <a name="debugging-code-overview"></a>调试代码概述

对于用户模式和内核模式驱动程序，可以使用特殊的调试例程、宏和全局变量。 通过在驱动程序代码中使用这些例程，你可以将消息发送到调试器并设置断点以帮助调试。

[条件编译和生成环境](conditional-compilation-and-the-build-environment.md)

有关调试的详细信息，请参阅文档中的以下主题：

[突入调试器](..\debugger\breaking-into-the-debugger.md)

[将输出发送到调试器](..\debugger\sending-output-to-the-debugger.md)

[读取和筛选调试消息](..\debugger\reading-and-filtering-debugging-messages.md)

[确定是否已附加调试器](..\debugger\determining-if-a-debugger-is-attached.md)
