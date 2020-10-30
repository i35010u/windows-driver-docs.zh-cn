---
title: 组件固件更新 (CFU)
description: 提供组件固件更新 (CFU) 的相关信息
ms.date: 10/01/2020
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: medium
ms.openlocfilehash: ad0ba908bf0705c9a9f25ea77b9601613ca59091
ms.sourcegitcommit: eefc6ae6d9621d0735b3c63e718ee5838d57a6bc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92886302"
---
# <a name="component-firmware-update-cfu"></a>组件固件更新 (CFU)

组件固件更新 (CFU) 向原始设备制造商 (OEM) 和独立硬件供应商 (IHV) 提供了一种经过身份验证的可靠方法来更新已发货给客户的设备上的固件。 此版本中有用于接收固件有效负载的参考固件。

有关 CFU 概念的介绍，请参阅[组件固件更新简介](https://blogs.windows.com/buildingapps/?p=54456)博客文章和 [WinHEC 2018 - 组件固件更新](https://developer.microsoft.com/windows/hardware/events)视频。

## <a name="in-this-section"></a>在本节中

| 主题 | 说明 |
|--|--|
| [CFU 固件实现指南](cfu-firmware-implementation-guide.md) | 提供详细指南来引导如何实现 CFU 固件协议以及创建要在目标设备上安装的新固件映像。 |
| [CFU INF 文件配置](cfu-inf-configuration.md) | 介绍如何为固件更新配置自定义设备 INF 文件。 |
| [CFU 协议规格](cfu-specification.md) | 提供有关 CFU 协议服务、内容和固件更新命令序列的详细信息。 |
| [CFU 独立工具](cfu-standalone-tool.md) | 介绍用于将固件更新映像文件发送到设备的 CFU 独立工具。 在开发期间和将固件更新上传到 Windows 更新之前，可使用此工具在设备上测试该固件更新。|
| [CFU 虚拟 HID 设备固件更新模拟](cfu-firmware-update-simulation.md) | 模拟在虚拟 HID 设备上更新固件的情况。 |
