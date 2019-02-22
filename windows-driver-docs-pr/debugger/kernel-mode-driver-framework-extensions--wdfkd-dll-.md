---
title: Windows 驱动程序框架扩展 (Wdfkd.dll)
description: Windows 驱动程序框架扩展 (Wdfkd.dll)
ms.assetid: 2fa2b131-f6fd-459b-a4e3-799246076338
keywords:
- 调试扩展 (wdfkd.dll) 内核模式驱动程序框架
- 内核模式驱动程序框架扩展 (wdfkd.dll)
- wdfkd.dll （内核模式驱动程序框架扩展）
- 扩展插件，内核模式驱动程序框架
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60d86f7b5473e3d39375fa7f5bfd571535f8782f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544953"
---
# <a name="windows-driver-framework-extensions-wdfkddll"></a>Windows 驱动程序框架扩展 (Wdfkd.dll)


可用于调试驱动程序使用内核模式驱动程序框架 (KMDF) 或版本 2 的用户模式驱动程序框架 (UMDF 2) 构建的扩展命令中 Wdfkd.dll 实现。

这些扩展可用于在 Microsoft Windows XP 和更高版本操作系统上。 某些扩展具有附加限制;在单独的参考页上说明了这些限制。

**请注意**  时创建新的 KMDF 或 UMDF 驱动程序，必须选择具有 32 个字符的驱动程序名称或更少。 此长度限制在 wdfglobals.h 中定义。 如果驱动程序名称超过了最大长度，您的驱动程序将无法加载。

 

有关如何使用这些扩展的详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

 

 





