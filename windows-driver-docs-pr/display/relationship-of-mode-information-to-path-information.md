---
title: 模式信息与路径信息之间的关系
description: 模式信息与路径信息之间的关系
ms.assetid: 214717dd-1c01-4daf-9296-586299668d3a
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
ms.openlocfilehash: 13d783f8b67164789ae860377a522e76b5b12e80
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715296"
---
# <a name="relationship-of-mode-information-to-path-information"></a>模式信息与路径信息之间的关系


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

[**QueryDisplayConfig**](/windows/win32/api/winuser/nf-winuser-querydisplayconfig) CCD 函数始终返回特定显示配置的路径信息以及源和目标模式信息。 下图显示了源和目标模式信息如何与路径信息相关的示例。 在此示例中，在 \_ \_ 调用**QUERYDISPLAYCONFIG**时，QDC 所有路径标记传递到*Flags*参数。

![说明模式信息与路径信息的关系的关系图](images/displayconfigpathandmode.png)

 

