---
title: 安装端口类音频适配器
description: 安装端口类音频适配器
ms.assetid: 02cea7c1-cf9a-4f4b-9d35-d565fac731ec
keywords:
- 端口类音频适配器 WDK，安装
- 音频的微型端口驱动程序 WDK，适配器驱动程序
- 微型端口驱动程序 WDK 音频，适配器驱动程序
- 适配器驱动程序 WDK 音频，安装
- 音频适配器驱动程序 WDK，安装
- 端口类音频适配器 WDK
- 注册表 WDK 音频
- 添加注册表部分 WDK 音频
- 音频适配器驱动程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42a8f94cbd0337e00daac007c7a0e428fffd7b7d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359888"
---
# <a name="installing-a-port-class-audio-adapter"></a>安装端口类音频适配器


## <span id="installing_a_port_class_audio_adapter"></span><span id="INSTALLING_A_PORT_CLASS_AUDIO_ADAPTER"></span>


本部分介绍在要安装的端口类音频适配器的 INF 文件中应包括供应商的特定于设备的类的信息。 有关常规的 INF 文件要求和选项的所有设备类的说明，请参阅[设备安装概述](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-device-and-driver-installation)。

在本部分中所需的 INF 文件条目的说明基于假设的 XYZ 音频设备。 此设备的驱动程序包含在一个名为 Xyzaudio.sys 文件中。 示例**制造商**并**模型**设备的部分如下所示：

```inf
  [VendorName]  ; Manufacturer section
  %XYZ-Audio-Device-Description%=XYZ-Audio-Device, <Plug and Play hardware ID>
  [XYZ-Audio-Device]  ; Models section
  AddReg=XYZ-Audio-Device.AddReg
```

有关详细信息，请参阅[ **INF AddReg 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)。

有关其他示例，请参阅 SYVAD 音频示例中包含的 INF 文件。 有关详细信息，请参阅[示例音频驱动程序](sample-audio-drivers.md)并[音频的通用 Windows 驱动程序](audio-universal-drivers.md)。

以下主题提供安装该设备的 INF 文件中的关键部分的示例：

[指定的音频的适配器的版本信息](specifying-version-information-for-an-audio-adapter.md)

[为音频适配器安装设备接口](installing-device-interfaces-for-an-audio-adapter.md)

[为音频适配器安装核心系统组件](installing-core-system-components-for-an-audio-adapter.md)

[安装 Windows 多媒体系统支持的音频的适配器](installing-windows-multimedia-system-support-for-an-audio-adapter.md)

[在 Windows 中安装的音频适配器服务](installing-an-audio-adapter-service-in-windows.md)

[自定义控制面板](customizing-control-panel.md)

[音频的适配器的其他安装问题](miscellaneous-installation-issues-for-an-audio-adapter.md)

 

 




