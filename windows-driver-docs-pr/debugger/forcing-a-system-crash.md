---
title: 强制系统崩溃
description: 强制系统崩溃
ms.assetid: db93b032-2ca7-4197-87dd-4ae77c328f60
keywords:
- 系统崩溃，概述
ms.date: 06/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 7e235df3c63b47efe9629faecb71e69a97d1ce21
ms.sourcegitcommit: 8097a09d2f989a9b3dca250c4e2ffd4cec2172e3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84563155"
---
# <a name="forcing-a-system-crash"></a>强制系统崩溃

[启用](enabling-a-kernel-mode-dump-file.md)内核模式转储文件后，大多数系统崩溃都应该导致写入崩溃文件并显示蓝屏。

但是，有时系统会冻结，而不会实际启动内核故障。 此类冻结的可能症状包括：

- 鼠标指针移动，但不能执行任何操作。

- 所有视频均已冻结，鼠标指针不会移动，但会继续分页。

- 对于鼠标或键盘，并没有任何使用磁盘的响应。

如果存在经验丰富的调试技术人员，则可以附加一个内核调试器并分析问题。 有关出现此情况时要查找的内容的一些提示，请参阅[调试停止的系统](debugging-a-stalled-system.md)。

但是，如果没有任何技术人员，你可能想要创建一个内核模式转储文件，并将其发送给非现场技术人员。 此转储文件可用于分析错误的原因。

有两种方法可以特意导致系统崩溃：

[通过调试器强制系统崩溃](forcing-a-system-crash-from-the-debugger.md)

[通过键盘强制系统崩溃](forcing-a-system-crash-from-the-keyboard.md)
