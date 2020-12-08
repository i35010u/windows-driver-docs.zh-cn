---
title: 适用于 windows 8 的 Windows 全新调试工具
description: 适用于 windows 8 的 Windows 全新调试工具
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c8c5439aa7a82ec9eff7f47d661fc7ebd24bb58
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819863"
---
# <a name="debugging-tools-for-windows-new-for-windows-8"></a>Windows 调试工具：Windows 8 的新增功能

从 Windows 8 开始，你可以从 Microsoft Visual Studio 开发、构建和调试内核模式和用户模式组件。 通过网络连接或 USB 3.0 连接增加了对调试的支持，并改进了对调试优化代码和内联函数的支持。 有关详细信息，请参阅以下主题：

-   [使用 Visual Studio 进行调试](debugging-using-visual-studio.md)
-   [手动设置网络连接](setting-up-a-network-debugging-connection.md)
-   [手动设置 USB 3.0 连接](setting-up-a-usb-3-0-debug-cable-connection.md)
-   [调试优化的代码和内联函数](debugging-optimized-code-and-inline-functions-external.md)

包括两组新的调试器扩展命令：

-   [USB 3.0 扩展](usb-3-extensions.md)
-   [RCDRKD 扩展](rcdrkd-extensions.md)

除了 Visual Studio，您还可以通过 sse Windows 调试器来调试 Windows 应用程序。 用于 Windows 的调试工具包包括 [**PLMDebug.exe**](plmdebug.md)，使你能够手动控制挂起、继续、调试和终止 Windows 应用程序。

Sos.dll 是用于调试托管代码的组件。 Windows 8 调试工具包不包含 sos.dll。 有关如何获取 sos.dll 的信息，请参阅在 [调试托管代码](debugging-managed-code.md) *( # A1) 获取 SOS 调试扩展*。

## <a name="related-topics"></a>相关主题

[Windows 调试](index.md)
