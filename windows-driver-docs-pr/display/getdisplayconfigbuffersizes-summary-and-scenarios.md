---
title: GetDisplayConfigBufferSizes 摘要和方案
description: GetDisplayConfigBufferSizes 摘要和方案
ms.assetid: b0d14ba7-fe61-49e9-81c5-097e6e07a51a
keywords:
- 连接显示 WDK Windows 7 显示、CCD Api、GetDisplayConfigBufferSizes
- 连接显示 WDK Windows Server 2008 R2 display、CCD Api、GetDisplayConfigBufferSizes
- 配置显示 WDK Windows 7 显示、CCD Api、GetDisplayConfigBufferSizes
- 配置显示 WDK Windows Server 2008 R2 display、CCD Api、GetDisplayConfigBufferSizes
- CCD 概念 WDK Windows 7 显示，GetDisplayConfigBufferSizes
- CCD 概念 WDK Windows Server 2008 R2 显示，GetDisplayConfigBufferSizes
- GetDisplayConfigBufferSizes WDK Windows 7 显示
- GetDisplayConfigBufferSizes WDK Windows Server 2008 R2 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e748ee6fbd00b2eb2b7a1f36785898d068e6920
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717216"
---
# <a name="getdisplayconfigbuffersizes-summary-and-scenarios"></a>GetDisplayConfigBufferSizes 摘要和方案


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

以下部分概述了调用方如何使用 [**GetDisplayConfigBufferSizes**](/windows/win32/api/winuser/nf-winuser-getdisplayconfigbuffersizes) CCD 函数并提供使用 **GetDisplayConfigBufferSizes**的方案。

### <a name="span-idgetdisplayconfigbuffersizes_summaryspanspan-idgetdisplayconfigbuffersizes_summaryspangetdisplayconfigbuffersizes-summary"></a><span id="getdisplayconfigbuffersizes_summary"></span><span id="GETDISPLAYCONFIGBUFFERSIZES_SUMMARY"></span>GetDisplayConfigBufferSizes 摘要

调用方可以使用 [**GetDisplayConfigBufferSizes**](/windows/win32/api/winuser/nf-winuser-getdisplayconfigbuffersizes) 来获取调用方需要用于 [**QueryDisplayConfig**](/windows/win32/api/winuser/nf-winuser-querydisplayconfig) CCD 函数的信息。

### <a name="span-idgetdisplayconfigbuffersizes_scenariosspanspan-idgetdisplayconfigbuffersizes_scenariosspangetdisplayconfigbuffersizes-scenarios"></a><span id="getdisplayconfigbuffersizes_scenarios"></span><span id="GETDISPLAYCONFIGBUFFERSIZES_SCENARIOS"></span>GetDisplayConfigBufferSizes 方案

调用[**QueryDisplayConfig**](/windows/win32/api/winuser/nf-winuser-querydisplayconfig)前始终会调用[**GetDisplayConfigBufferSizes**](/windows/win32/api/winuser/nf-winuser-getdisplayconfigbuffersizes) 。

 

