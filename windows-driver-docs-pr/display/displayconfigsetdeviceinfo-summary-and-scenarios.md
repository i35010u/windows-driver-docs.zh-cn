---
title: DisplayConfigSetDeviceInfo 摘要和方案
description: DisplayConfigSetDeviceInfo 摘要和方案
ms.assetid: b00c1586-26f0-4fe1-8cc8-3db552ebba86
keywords:
- 连接显示 WDK Windows 7 显示、CCD Api、DisplayConfigSetDeviceInfo
- 连接显示 WDK Windows Server 2008 R2 display、CCD Api、DisplayConfigSetDeviceInfo
- 配置显示 WDK Windows 7 显示、CCD Api、DisplayConfigSetDeviceInfo
- 配置显示 WDK Windows Server 2008 R2 display、CCD Api、DisplayConfigSetDeviceInfo
- CCD 概念 WDK Windows 7 显示，DisplayConfigSetDeviceInfo
- CCD 概念 WDK Windows Server 2008 R2 显示，DisplayConfigSetDeviceInfo
- DisplayConfigSetDeviceInfo WDK Windows 7 显示
- DisplayConfigSetDeviceInfo WDK Windows Server 2008 R2 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3785cc290ec6bb92ed0d840c8b9bb7878783aece
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716282"
---
# <a name="displayconfigsetdeviceinfo-summary-and-scenarios"></a>DisplayConfigSetDeviceInfo 摘要和方案


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

以下部分概述了调用方如何使用 [**DisplayConfigSetDeviceInfo**](/windows/win32/api/winuser/nf-winuser-displayconfigsetdeviceinfo) CCD 函数并提供使用 **DisplayConfigSetDeviceInfo**的方案。

### <a name="span-iddisplayconfigsetdeviceinfo_summaryspanspan-iddisplayconfigsetdeviceinfo_summaryspandisplayconfigsetdeviceinfo-summary"></a><span id="displayconfigsetdeviceinfo_summary"></span><span id="DISPLAYCONFIGSETDEVICEINFO_SUMMARY"></span>DisplayConfigSetDeviceInfo 摘要

调用方可以使用 [**DisplayConfigSetDeviceInfo**](/windows/win32/api/winuser/nf-winuser-displayconfigsetdeviceinfo) 设置目标的属性。 **DisplayConfigSetDeviceInfo** 仅可用于启动和停止模拟目标上的启动持久化强制投影。

### <a name="span-iddisplayconfigsetdeviceinfo_scenariosspanspan-iddisplayconfigsetdeviceinfo_scenariosspandisplayconfigsetdeviceinfo-scenarios"></a><span id="displayconfigsetdeviceinfo_scenarios"></span><span id="DISPLAYCONFIGSETDEVICEINFO_SCENARIOS"></span>DisplayConfigSetDeviceInfo 方案

在以下情况下，将调用[**DisplayConfigSetDeviceInfo**](/windows/win32/api/winuser/nf-winuser-displayconfigsetdeviceinfo) ：

-   假设用户使用 S-视频或复合连接器连接电视，并且操作系统无法检测到电视。 显示控制面板小程序可以调用 [**DisplayConfigSetDeviceInfo**](/windows/win32/api/winuser/nf-winuser-displayconfigsetdeviceinfo) 来强制执行连接器上的输出。

-   假设用户使用了 switchbox 或 KVM 交换机，并且操作系统无法从监视器读取 EDID。 显示控制面板小程序可以调用 [**DisplayConfigSetDeviceInfo**](/windows/win32/api/winuser/nf-winuser-displayconfigsetdeviceinfo) 来强制连接器上的输出，并设置分辨率。

 

