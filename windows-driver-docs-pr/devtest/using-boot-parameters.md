---
title: 使用启动参数
description: 使用启动参数
ms.assetid: f249f312-cfc5-41b2-ad67-75497a929e35
keywords:
- 启动条目 WDK
- 启动选项 WDK，启动参数
- 驱动程序测试 WDK 启动选项
- 测试驱动程序 WDK 启动选项
- 调试驱动程序 WDK 启动选项
- 驱动程序调试 WDK 启动选项
- NVRAM 启动选项 WDK，启动参数
- EFI NVRAM 启动选项 WDK，启动参数
- Boot.ini 文件 WDK，启动参数
ms.date: 06/04/2020
ms.localizationpriority: medium
ms.openlocfilehash: 893aacd257d1333bf1163d5f34faf388c3c1330d
ms.sourcegitcommit: 0a0b75d93130b6c5854279607cd0aac099f65fd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2020
ms.locfileid: "84428344"
---
# <a name="using-boot-parameters"></a>使用启动参数

通常，驱动程序开发人员和测试人员需要添加、删除和更改启动项的参数，以便在可变条件下测试其驱动程序。 本部分介绍几个常见方案，并提供在 Boot.ini 文件和 NVRAM 中配置启动参数的策略。

> [!NOTE]
> 在 Windows 10 版本1803之前，已检查的生成在较早版本的 Windows 上可用。
> 使用驱动程序验证程序和 GFlags 等工具在更高版本的 Windows 中检查驱动程序代码。

本节包含下列主题：

[用于启用调试的启动参数](boot-parameters-to-enable-debugging.md)

[用于操作内存的启动参数](boot-parameters-to-manipulate-memory.md)

[用于加载部分已检验版本的启动参数](boot-parameters-to-load-a-partial-checked-build.md)

[用于启用 EMS 重定向的启动参数](boot-parameters-to-enable-ems-redirection.md)

[用于配置 DEP 和 PAE 的启动参数](boot-parameters-to-configure-dep-and-pae.md)
