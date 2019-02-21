---
title: 安装 Windows 多媒体系统支持的音频的适配器
description: 安装 Windows 多媒体系统支持的音频的适配器
ms.assetid: 5846404f-3a6a-4e55-ba83-18404ea7cace
keywords:
- 音频适配器 WDK、 多媒体支持
- 适配器驱动程序 WDK 音频、 多媒体支持
- 端口类音频适配器 WDK、 多媒体支持
- 多媒体 WDK 音频
- Windows 多媒体支持 WDK 音频
ms.date: 10/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a01293d8d5ab3e25fc2f25abb68fdc28eda9729
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548175"
---
# <a name="installing-windows-multimedia-system-support-for-an-audio-adapter"></a>安装 Windows 多媒体系统支持的音频的适配器


## <span id="ddk_installing_windows_multimedia_system_support_for_an_audio_adapter_"></span><span id="DDK_INSTALLING_WINDOWS_MULTIMEDIA_SYSTEM_SUPPORT_FOR_AN_AUDIO_ADAPTER_"></span>


INF 添加注册表部分创建或修改系统注册表中的特定于驱动程序的信息。 PortCls 音频适配器的添加注册表部分包含允许适配器访问的 Windows 多媒体系统组件的信息。

以下示例显示了添加注册表部分中，x y Z-音频-Device.AddReg，在名为[ **INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)上一示例中 (请参阅[安装端口类音频适配器](installing-a-port-class-audio-adapter.md)):

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

添加注册表部分将添加指定系统需要加载，以便 Windows 多媒体系统可以使用音频的适配器的组件的注册表项。 这些组件包括适配器驱动程序、 Xyzaud.sys 和系统驱动程序 WDMAud、 SWMidi 和 Redbook (请参阅[内核模式 WDM 音频组件](kernel-mode-wdm-audio-components.md))。

**AssociatedFilters**示例添加注册表部分中的关键字指示指令包含其加载是延迟，直到它们所需的适配器驱动程序的一个或多个辅助驱动程序文件的名称。 替代方法是加载设备驱动程序的同时加载辅助文件。

 

 




