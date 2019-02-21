---
title: INF GeneralConfigData Section
description: INF GeneralConfigData Section
ms.assetid: 49b00396-479f-471a-8c79-bb8ef33ebcaa
keywords:
- GeneralConfigData 部分
- INF 文件 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d374a91642d4eef7e36bd05e1b3472ef16735762
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546685"
---
# <a name="inf-generalconfigdata-section"></a>INF GeneralConfigData Section


## <span id="ddk_inf_generalconfigdata_section_gg"></span><span id="DDK_INF_GENERALCONFIGDATA_SECTION_GG"></span>


如果您的微型端口驱动程序映射多个 8 MB 中的设备内存，包括**GeneralConfigData** INF 文件中的部分。

```inf
[GeneralConfigData]

[MaximumDeviceMemoryConfiguration = n]
[MaximumNumberOfDevices = n]
```

以下是**GeneralConfigData**条目和值：

<span id="MaximumDeviceMemoryConfiguration_n"></span><span id="maximumdevicememoryconfiguration_n"></span><span id="MAXIMUMDEVICEMEMORYCONFIGURATION_N"></span>**MaximumDeviceMemoryConfiguration**=*n*  
指定的微型端口驱动程序将尝试将映射到枚举的 PCI 视频设备的系统地址空间的设备内存兆字节为单位的最大数目。 Windows 使用此值作为提示，以确定它映射为应分配多少系统页表项 (Pte)。 此项才会生效，可能需要重新启动。 您可以确定是否重新启动是必需的检查你的设备在设备管理器的状态。

<span id="MaximumNumberOfDevices_n"></span><span id="maximumnumberofdevices_n"></span><span id="MAXIMUMNUMBEROFDEVICES_N"></span>**MaximumNumberOfDevices**=*n*  
指定多少个视频设备 （如 PCI 的枚举和取决于您的微型端口驱动程序） 都将是系统中。 如果指定此项，则还必须指定**MaximumDeviceMemoryConfiguration**条目。 此项才会生效，可能需要重新启动。 您可以确定是否重新启动是必需的检查你的设备在设备管理器的状态。

有关支持多个监视器的信息，请参阅[支持双视图 （Windows 2000 模式）](supporting-dualview--windows-2000-model-.md)并[显示器驱动程序中的多监视器支持](multiple-monitor-support-in-the-display-driver.md)。









