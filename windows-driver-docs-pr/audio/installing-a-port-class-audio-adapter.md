---
title: 安装端口类音频适配器
description: 安装端口类音频适配器
keywords:
- 端口类音频适配器 WDK，安装
- 音频微型端口驱动程序 WDK，适配器驱动程序
- 微型端口驱动程序 WDK 音频，适配器驱动程序
- 适配器驱动程序 WDK 音频，安装
- 音频适配器驱动程序 WDK，安装
- 端口类音频适配器 WDK
- 注册表 WDK 音频
- 添加注册表部分 WDK 音频
- 音频适配器驱动程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3489ed322613c1010df24886d4ad777ae5b8e9c8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799249"
---
# <a name="installing-a-port-class-audio-adapter"></a>安装端口类音频适配器


## <span id="installing_a_port_class_audio_adapter"></span><span id="INSTALLING_A_PORT_CLASS_AUDIO_ADAPTER"></span>


本部分介绍特定于设备类的信息，供应商应在 INF 文件中包含该信息以安装端口级音频适配器。 有关所有设备类的常规 INF 文件要求和选项的说明，请参阅 [设备安装概述](../install/overview-of-device-and-driver-installation.md)。

本节中所需 INF 文件条目的说明基于假设的 XYZ 音频设备。 此设备的驱动程序包含在名为 Xyzaudio.sys 的文件中。 设备的示例 **制造商** 和 **型号** 部分如下所示：

```inf
  [VendorName]  ; Manufacturer section
  %XYZ-Audio-Device-Description%=XYZ-Audio-Device, <Plug and Play hardware ID>
  [XYZ-Audio-Device]  ; Models section
  AddReg=XYZ-Audio-Device.AddReg
```

有关详细信息，请参阅 [**INF AddReg 指令**](../install/inf-addreg-directive.md)。

有关其他示例，请参阅 SYVAD 音频示例中包含的 INF 文件。 有关详细信息，请参阅音频的 [示例音频驱动](sample-audio-drivers.md) 程序和 [通用 Windows 驱动程序](audio-universal-drivers.md)。

以下主题提供了用于安装设备的 INF 文件中的关键部分的示例：

[指定音频适配器的版本信息](specifying-version-information-for-an-audio-adapter.md)

[为音频适配器安装设备接口](installing-device-interfaces-for-an-audio-adapter.md)

[为音频适配器安装核心系统组件](installing-core-system-components-for-an-audio-adapter.md)

[为音频适配器安装 Windows 多媒体系统支持](installing-windows-multimedia-system-support-for-an-audio-adapter.md)

[在 Windows 中安装音频适配器服务](installing-an-audio-adapter-service-in-windows.md)

[自定义控制面板](customizing-control-panel.md)

[音频适配器的其他安装问题](miscellaneous-installation-issues-for-an-audio-adapter.md)

 

