---
title: DisplayConfigSetDeviceInfo 摘要和方案
description: DisplayConfigSetDeviceInfo 摘要和方案
ms.assetid: b00c1586-26f0-4fe1-8cc8-3db552ebba86
keywords:
- 连接显示 WDK Windows 7 显示 DisplayConfigSetDeviceInfo 在 CCD Api
- 连接显示 WDK Windows Server 2008 R2 显示 DisplayConfigSetDeviceInfo 在 CCD Api
- 配置显示 WDK Windows 7 显示 DisplayConfigSetDeviceInfo 在 CCD Api
- 配置显示 WDK Windows Server 2008 R2 显示 DisplayConfigSetDeviceInfo 在 CCD Api
- CCD 概念 WDK Windows 7 显示 DisplayConfigSetDeviceInfo
- CCD 概念 WDK Windows Server 2008 R2 显示 DisplayConfigSetDeviceInfo
- DisplayConfigSetDeviceInfo WDK Windows 7 显示
- DisplayConfigSetDeviceInfo WDK Windows Server 2008 R2 display
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18d4d4cc1986671e724bd9554fef8ac91b6fc0b3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522234"
---
# <a name="displayconfigsetdeviceinfo-summary-and-scenarios"></a>DisplayConfigSetDeviceInfo 摘要和方案


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

以下部分汇总了如何使用调用方[ **DisplayConfigSetDeviceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff553909) CCD 函数，并提供了有关使用方案**DisplayConfigSetDeviceInfo**。

### <a name="span-iddisplayconfigsetdeviceinfosummaryspanspan-iddisplayconfigsetdeviceinfosummaryspandisplayconfigsetdeviceinfo-summary"></a><span id="displayconfigsetdeviceinfo_summary"></span><span id="DISPLAYCONFIGSETDEVICEINFO_SUMMARY"></span>DisplayConfigSetDeviceInfo Summary

可以使用调用方[ **DisplayConfigSetDeviceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff553909)设置的目标属性。 **DisplayConfigSetDeviceInfo**仅当前可用来启动和停止启动持久化模拟目标上的 force 投影。

### <a name="span-iddisplayconfigsetdeviceinfoscenariosspanspan-iddisplayconfigsetdeviceinfoscenariosspandisplayconfigsetdeviceinfo-scenarios"></a><span id="displayconfigsetdeviceinfo_scenarios"></span><span id="DISPLAYCONFIGSETDEVICEINFO_SCENARIOS"></span>DisplayConfigSetDeviceInfo Scenarios

[**DisplayConfigSetDeviceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff553909)在以下情况下调用：

-   假设用户使用 S-视频或复合连接器来连接电视，并且操作系统是无法检测到电视。 显示控制面板小程序可以调用[ **DisplayConfigSetDeviceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff553909)的连接器上强制输出。

-   假设用户使用一个交换盒或 KVM 交换机，并且操作系统不能以读取来自监视器 EDID。 显示控制面板小程序可以调用[ **DisplayConfigSetDeviceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff553909)以强制进行的连接器上输出并设置分辨率。

 

 





