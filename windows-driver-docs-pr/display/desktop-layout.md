---
title: 桌面布局
description: 桌面布局
ms.assetid: f1c074ec-2fce-4e46-ba0d-62e05ca8a9e7
keywords:
- 连接显示 WDK Windows 7 显示、CCD 概念、桌面布局
- 连接显示 WDK Windows Server 2008 R2 显示、CCD 概念、桌面布局
- 配置显示 WDK Windows 7 显示、CCD 概念、桌面布局
- 配置显示 WDK Windows Server 2008 R2 显示、CCD 概念、桌面布局
- CCD 概念 WDK Windows 7 显示，桌面布局
- CCD 概念 WDK Windows Server 2008 R2 显示，桌面布局
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b86d7c466fcce086c74499e36bdaddaa97c9551
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717238"
---
# <a name="desktop-layout"></a>桌面布局


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

调用方在对[**SetDisplayConfig**](/windows/win32/api/winuser/nf-winuser-setdisplayconfig) CCD 函数的调用中使用[**DISPLAYCONFIG \_ 源 \_ 模式**](/windows/win32/api/wingdi/ns-wingdi-displayconfig_source_mode)结构的**位置**成员来控制桌面上源表面的排列。 **位置**成员指定源图面的左上角的桌面坐标中的位置。 位于 (0，0) 的源图面视为主要面。 GDI 严格规定了如何在桌面空间中排列源表面。 例如，GDI 不允许源表面之间的任何间隔，也不允许在源表面之间重叠。

尽管 [**SetDisplayConfig**](/windows/win32/api/winuser/nf-winuser-setdisplayconfig) 尝试重排源表面来强制执行这些 GDI 布局规则，但调用方应指定源表面的布局。 不确定 GDI 如何重排源表面来强制执行其布局规则，并且源表面的生成布局可能不是调用方要实现的目标。

 

