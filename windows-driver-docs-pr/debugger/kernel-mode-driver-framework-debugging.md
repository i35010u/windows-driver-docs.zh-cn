---
title: 内核模式驱动程序框架调试
description: 内核模式驱动程序框架调试
ms.assetid: bec840f8-b500-464f-8e49-53f03f34aa6a
keywords:
- 内核模式驱动程序框架调试
- Windows Driver Foundation
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 035e3f133e113bb9501413a954a8eb8283bc53c3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367201"
---
# <a name="kernel-mode-driver-framework-debugging"></a>内核模式驱动程序框架调试


调试扩展内核模式驱动程序框架 (KMDF) 包含在 Wdfkd.dll 扩展库中。

可以使用调试驱动程序的使用 KMDF 包含 Wdfkd.dll 扩展库扩展命令。

Wdfkd.dll 中的扩展命令的说明，请参阅[内核模式驱动程序框架扩展 (Wdfkd.dll)](kernel-mode-driver-framework-extensions--wdfkd-dll-.md)。

这些扩展可用于在 Microsoft Windows XP 和更高版本操作系统上。 某些扩展具有附加限制;在单独的参考页上说明了这些限制。

**注意**  在创建新的 KMDF 或 UMDF 驱动程序时，必须选择一个不多于 32 个字符的驱动程序名称。 此长度限制在 wdfglobals.h 中定义。 如果驱动程序名称超过了最大长度，您的驱动程序将无法加载。

 

若要使用此扩展插件库，必须在库加载到调试器中。 有关如何将扩展库加载到调试器的信息，请参阅[加载的调试器扩展 Dll](loading-debugger-extension-dlls.md)。

 

 





