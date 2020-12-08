---
title: Windows 驱动程序框架扩展 (Wdfkd.dll)
description: Windows 驱动程序框架扩展 (Wdfkd.dll)
keywords:
- 'Kernel-Mode Driver Framework 调试，扩展 ( # A0) '
- 'Kernel-Mode Driver Framework 扩展 ( # A0) '
- 'wdfkd.dll (内核模式驱动程序框架扩展) '
- 扩展，Kernel-Mode Driver Framework
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: fac2e302319349bc28a58168dd806319d0a64bc6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801905"
---
# <a name="windows-driver-framework-extensions-wdfkddll"></a>Windows 驱动程序框架扩展 (Wdfkd.dll)


在 (中实现了用于调试用 Kernel-Mode Driver Framework (KMDF) 或版本2的 User-Mode 驱动程序框架构建的驱动程序的扩展命令) 。

这些扩展可在 Microsoft Windows XP 和更高版本的操作系统上使用。 某些扩展具有其他限制;这些限制在各个参考页上注明。

**注意**  在创建新的 KMDF 或 UMDF 驱动程序时，必须选择一个不多于 32 个字符的驱动程序名称。 此长度限制在 wdfglobals.h 中定义。 如果你的驱动程序名称超出最大长度，则你的驱动程序将无法加载。

 

有关如何使用这些扩展的详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

 

 





