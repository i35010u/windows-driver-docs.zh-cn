---
title: DisplayConfigGetDeviceInfo 摘要和方案
description: DisplayConfigGetDeviceInfo 摘要和方案
ms.assetid: 19d9a77c-252e-4623-b4bc-f0b990ed31e2
keywords:
- 连接显示 WDK Windows 7 显示、CCD Api、DisplayConfigGetDeviceInfo
- 连接显示 WDK Windows Server 2008 R2 display、CCD Api、DisplayConfigGetDeviceInfo
- 配置显示 WDK Windows 7 显示、CCD Api、DisplayConfigGetDeviceInfo
- 配置显示 WDK Windows Server 2008 R2 display、CCD Api、DisplayConfigGetDeviceInfo
- CCD 概念 WDK Windows 7 显示，DisplayConfigGetDeviceInfo
- CCD 概念 WDK Windows Server 2008 R2 显示，DisplayConfigGetDeviceInfo
- DisplayConfigGetDeviceInfo WDK Windows 7 显示
- DisplayConfigGetDeviceInfo WDK Windows Server 2008 R2 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cbfd8dd03791a70381da1f659bef436b67cc0f6
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716288"
---
# <a name="displayconfiggetdeviceinfo-summary-and-scenarios"></a>DisplayConfigGetDeviceInfo 摘要和方案


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

以下部分概述了调用方如何使用 [**DisplayConfigGetDeviceInfo**](/windows/win32/api/winuser/nf-winuser-displayconfiggetdeviceinfo) CCD 函数并提供使用 **DisplayConfigGetDeviceInfo**的方案。

### <a name="span-iddisplayconfiggetdeviceinfo_summaryspanspan-iddisplayconfiggetdeviceinfo_summaryspandisplayconfiggetdeviceinfo-summary"></a><span id="displayconfiggetdeviceinfo_summary"></span><span id="DISPLAYCONFIGGETDEVICEINFO_SUMMARY"></span>DisplayConfigGetDeviceInfo 摘要

调用方可以使用 [**DisplayConfigGetDeviceInfo**](/windows/win32/api/winuser/nf-winuser-displayconfiggetdeviceinfo) 获取更友好的名称，以在用户界面中显示。 调用方可以获取适配器、源和目标的名称。 调用方还可以使用 **DisplayConfigGetDeviceInfo** 来获取连接的显示设备的本机分辨率。

### <a name="span-iddisplayconfiggetdeviceinfo_scenariosspanspan-iddisplayconfiggetdeviceinfo_scenariosspandisplayconfiggetdeviceinfo-scenarios"></a><span id="displayconfiggetdeviceinfo_scenarios"></span><span id="DISPLAYCONFIGGETDEVICEINFO_SCENARIOS"></span>DisplayConfigGetDeviceInfo 方案

在以下情况下，将调用[**DisplayConfigGetDeviceInfo**](/windows/win32/api/winuser/nf-winuser-displayconfiggetdeviceinfo) ：

-   显示控制面板小程序调用 [**DisplayConfigGetDeviceInfo**](/windows/win32/api/winuser/nf-winuser-displayconfiggetdeviceinfo) ，以获取要在列出所有连接的监视器的下拉菜单中显示的监视器名称。

-   显示控制面板小程序调用 [**DisplayConfigGetDeviceInfo**](/windows/win32/api/winuser/nf-winuser-displayconfiggetdeviceinfo) 以获取连接到系统的适配器的名称。

-   显示控制面板小程序调用 [**DisplayConfigGetDeviceInfo**](/windows/win32/api/winuser/nf-winuser-displayconfiggetdeviceinfo) 来获取每个连接的监视器的本机分辨率，以便可以在用户界面中突出显示分辨率。

 

