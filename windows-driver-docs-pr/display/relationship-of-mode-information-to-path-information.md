---
title: 模式信息与路径信息之间的关系
description: 模式信息与路径信息之间的关系
keywords:
- 连接显示 WDK Windows 7 显示、CCD 概念、模式和路径信息
- 正在连接显示 WDK Windows Server 2008 R2 显示、CCD 的概念、模式和路径信息
- 配置显示 WDK Windows 7 显示、CCD 概念、模式和路径信息
- 配置显示 WDK Windows Server 2008 R2 显示、CCD 概念、模式和路径信息
- CCD 概念 WDK Windows 7 显示、模式和路径信息
- CCD 概念 WDK Windows Server 2008 R2 显示、模式和路径信息
- 模式和路径信息 WDK Windows 7 显示
- 模式和路径信息 WDK Windows Server 2008 R2 显示
- 路径和模式信息 WDK Windows 7 显示
- 路径和模式信息 WDK Windows Server 2008 R2 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 416730148d17c6e2bdfa7249fc71c1deeb737151
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825727"
---
# <a name="relationship-of-mode-information-to-path-information"></a>模式信息与路径信息之间的关系


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

[**QueryDisplayConfig**](/windows/win32/api/winuser/nf-winuser-querydisplayconfig) CCD 函数始终返回特定显示配置的路径信息以及源和目标模式信息。 下图显示了源和目标模式信息如何与路径信息相关的示例。 在此示例中，在 \_ \_ 调用 **QUERYDISPLAYCONFIG** 时，QDC 所有路径标记传递到 *Flags* 参数。

![说明模式信息与路径信息的关系的关系图](images/displayconfigpathandmode.png)

 

