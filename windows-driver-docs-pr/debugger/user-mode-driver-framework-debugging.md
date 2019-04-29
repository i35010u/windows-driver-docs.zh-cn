---
title: 用户模式驱动程序框架调试
description: 用户模式驱动程序框架调试
ms.assetid: f59a420e-57d3-4ae0-84e3-58ec6e088b63
keywords:
- 调试用户模式驱动程序框架
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6982feb6288937c5cf25dd7fbebab39603cf50b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368103"
---
# <a name="user-mode-driver-framework-debugging"></a>用户模式驱动程序框架调试


有关如何调试用户模式驱动程序框架 (UMDF) 驱动程序，包括如何启动调试会话中，此类信息的概述，请参阅[调试 UMDF 驱动程序](https://go.microsoft.com/fwlink/p/?linkid=153578)Windows Driver Kit (WDK) 文档的部分。

### <a name="span-idumdfdebuggingextensionsspanspan-idumdfdebuggingextensionsspanumdf-debugging-extensions"></a><span id="umdf_debugging_extensions"></span><span id="UMDF_DEBUGGING_EXTENSIONS"></span>UMDF 调试扩展

扩展模块 Wudfext.dll 中实现用户模式驱动程序框架 (UMDF) 调试扩展。 这些扩展可用于调试使用 UMDF 驱动程序。

Wudfext.dll 中的扩展命令的完整说明，请参阅[用户模式驱动程序框架扩展 (Wudfext.dll)](user-mode-driver-framework-extensions--wudfext-dll-.md)。

某些扩展具有 UMDF 是必需的; 的版本的 Windows 版本上的其他限制在单独的参考页上说明了这些限制。

**注意**  在创建新的 KMDF 或 UMDF 驱动程序时，必须选择一个不多于 32 个字符的驱动程序名称。 此长度限制在 wdfglobals.h 中定义。 如果驱动程序名称超过了最大长度，您的驱动程序将无法加载。

 

若要使用此扩展插件库，必须在库加载到调试器中。 有关如何将扩展库加载到调试器的信息，请参阅[加载的调试器扩展 Dll](loading-debugger-extension-dlls.md)。

 

 





