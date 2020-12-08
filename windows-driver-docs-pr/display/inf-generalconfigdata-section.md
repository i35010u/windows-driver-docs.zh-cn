---
title: INF GeneralConfigData 节
description: INF GeneralConfigData 节
keywords:
- GeneralConfigData 部分
- INF 文件 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 310147f6c166f6364cd0d6759cbe9876d7bc502f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827267"
---
# <a name="inf-generalconfigdata-section"></a>INF GeneralConfigData 节


## <span id="ddk_inf_generalconfigdata_section_gg"></span><span id="DDK_INF_GENERALCONFIGDATA_SECTION_GG"></span>


如果微型端口驱动程序映射的设备内存超过 8 MB，请在 INF 文件中包含 **GeneralConfigData** 部分。

```inf
[GeneralConfigData]

[MaximumDeviceMemoryConfiguration = n]
[MaximumNumberOfDevices = n]
```

下面是 **GeneralConfigData** 项和值：

<span id="MaximumDeviceMemoryConfiguration_n"></span><span id="maximumdevicememoryconfiguration_n"></span><span id="MAXIMUMDEVICEMEMORYCONFIGURATION_N"></span>**MaximumDeviceMemoryConfiguration** =*n*  
指定微型端口驱动程序将尝试映射到 PCI 所枚举的一个视频设备的系统地址空间的最大大小（mb）。 Windows 使用此值作为提示来确定应为映射分配 (Pte) 多少个系统页表项。 要使此项生效，可能需要重新启动。 可以通过在设备管理器中检查设备的状态来确定是否需要重新启动。

<span id="MaximumNumberOfDevices_n"></span><span id="maximumnumberofdevices_n"></span><span id="MAXIMUMNUMBEROFDEVICES_N"></span>**MaximumNumberOfDevices** =*n*  
指定由 PCI 枚举并由微型端口驱动程序驱动) 应在系统中出现的视频设备 (数量。 如果指定此项，则还必须指定 **MaximumDeviceMemoryConfiguration** 项。 要使此项生效，可能需要重新启动。 可以通过在设备管理器中检查设备的状态来确定是否需要重新启动。

有关支持多个监视器的信息，请参阅[在显示驱动程序中](multiple-monitor-support-in-the-display-driver.md)[支持双屏 (Windows 2000 模型) ](supporting-dualview--windows-2000-model-.md)和多监视器支持。









