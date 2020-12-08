---
title: GetDisplayConfigBufferSizes 摘要和方案
description: GetDisplayConfigBufferSizes 摘要和方案
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
ms.openlocfilehash: 6e0e442ef81815cc51632554d345e56cc79f36e9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786879"
---
# <a name="getdisplayconfigbuffersizes-summary-and-scenarios"></a>GetDisplayConfigBufferSizes 摘要和方案


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

以下部分概述了调用方如何使用 [**GetDisplayConfigBufferSizes**](/windows/win32/api/winuser/nf-winuser-getdisplayconfigbuffersizes) CCD 函数并提供使用 **GetDisplayConfigBufferSizes** 的方案。

### <a name="span-idgetdisplayconfigbuffersizes_summaryspanspan-idgetdisplayconfigbuffersizes_summaryspangetdisplayconfigbuffersizes-summary"></a><span id="getdisplayconfigbuffersizes_summary"></span><span id="GETDISPLAYCONFIGBUFFERSIZES_SUMMARY"></span>GetDisplayConfigBufferSizes 摘要

调用方可以使用 [**GetDisplayConfigBufferSizes**](/windows/win32/api/winuser/nf-winuser-getdisplayconfigbuffersizes) 来获取调用方需要用于 [**QueryDisplayConfig**](/windows/win32/api/winuser/nf-winuser-querydisplayconfig) CCD 函数的信息。

### <a name="span-idgetdisplayconfigbuffersizes_scenariosspanspan-idgetdisplayconfigbuffersizes_scenariosspangetdisplayconfigbuffersizes-scenarios"></a><span id="getdisplayconfigbuffersizes_scenarios"></span><span id="GETDISPLAYCONFIGBUFFERSIZES_SCENARIOS"></span>GetDisplayConfigBufferSizes 方案

调用 [**QueryDisplayConfig**](/windows/win32/api/winuser/nf-winuser-querydisplayconfig)前始终会调用 [**GetDisplayConfigBufferSizes**](/windows/win32/api/winuser/nf-winuser-getdisplayconfigbuffersizes) 。

 

