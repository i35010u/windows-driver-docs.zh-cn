---
title: 为音频适配器安装 Windows 多媒体系统支持
description: 为音频适配器安装 Windows 多媒体系统支持
keywords:
- 音频适配器 WDK，多媒体支持
- 适配器驱动程序 WDK 音频，多媒体支持
- 端口类音频适配器 WDK，多媒体支持
- 多媒体 WDK 音频
- Windows 多媒体支持 WDK 音频
ms.date: 10/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff1480fcaee29a0e7b2dc7a041c067284ff1c3fa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784731"
---
# <a name="installing-windows-multimedia-system-support-for-an-audio-adapter"></a>为音频适配器安装 Windows 多媒体系统支持


## <span id="ddk_installing_windows_multimedia_system_support_for_an_audio_adapter_"></span><span id="DDK_INSTALLING_WINDOWS_MULTIMEDIA_SYSTEM_SUPPORT_FOR_AN_AUDIO_ADAPTER_"></span>


INF 外接程序部分在系统注册表中创建或修改特定于驱动程序的信息。 PortCls 音频适配器的 "添加注册表" 部分包含的信息使适配器可供 Windows 多媒体系统组件访问。

下面的示例演示了在前面的 (示例中的 [**INF AddReg 指令**](../install/inf-addreg-directive.md) 中命名的 "AddReg" 外接程序部分，请参阅 [安装端口类音频适配器](installing-a-port-class-audio-adapter.md)) ：

```cpp
  [XYZ-Audio-Device.AddReg]
  HKR,,AssociatedFilters,,"wdmaud,swmidi,redbook"
  HKR,,Driver,,xyzaud.sys 
  HKR,Drivers,SubClasses,,"wave,midi,mixer,aux"

  HKR,Drivers\wave\Wdmaud.drv,Driver,,Wdmaud.drv
  HKR,Drivers\midi\Wdmaud.drv,Driver,,Wdmaud.drv
  HKR,Drivers\mixer\Wdmaud.drv,Driver,,Wdmaud.drv
  HKR,Drivers\aux\Wdmaud.drv,Driver,,Wdmaud.drv

  HKR,Drivers\wave\Wdmaud.drv,Description,,%XYZ-Audio-Device-Description%
  HKR,Drivers\midi\Wdmaud.drv,Description,,%XYZ-Audio-Device-Description%
  HKR,Drivers\mixer\Wdmaud.drv,Description,,%XYZ-Audio-Device-Description%
  HKR,Drivers\aux\Wdmaud.drv,Description,,%XYZ-Audio-Device-Description%
```

"添加注册表" 部分添加了用于指定系统需要加载的组件的注册表项，以便 Windows 多媒体系统可以使用音频适配器。 这些组件包括适配器驱动程序、Xyzaud.sys 以及系统驱动程序 WDMAud、SWMidi 和 Redbook (参阅 [内核模式 WDM 音频组件](kernel-mode-wdm-audio-components.md)) 。

示例 "添加注册表" 部分中的 **AssociatedFilters** 关键字指示指令包含一个或多个辅助驱动程序文件的名称，这些辅助驱动程序文件的加载将推迟到适配器驱动程序需要它们时进行推迟。 替代方法是在加载设备驱动程序的同时加载辅助文件。

 

