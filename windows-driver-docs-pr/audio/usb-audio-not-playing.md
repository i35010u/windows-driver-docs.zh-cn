---
title: USB 音频未播放
description: 音频驱动程序事件集
ms.assetid: ee800f71-9c90-4084-b879-32300e6706fc
ms.date: 12/19/2019
ms.localizationpriority: medium
ms.openlocfilehash: 84331325f386adb28a53a9224b1c9a20ab9d2bfb
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606631"
---
# <a name="usb-audio-not-playing-kb-4045958-audio-services-not-responding-error-and-usb-audio-device-does-not-work-in-windows-10-version-1703"></a>USB 音频未播放（KB 4045958） "音频服务未响应" 错误和 USB 音频设备在 Windows 10 版本1703中无法正常工作

## <a name="symptoms"></a>症状

请考虑以下方案：

1. 首次将通用串行总线（USB）音频设备（如音频适配器或 USB 数字到模拟转换器（DAC））连接到基于 Windows 10 版本1703的计算机。
2. 操作系统检测设备并加载标准 USB 音频2.0 驱动程序（usbaudio2）。
3. 然后，Windows 从 Windows 更新下载设备特定驱动程序。  
4. 下载的设备驱动程序将替换 usbaudio2 驱动程序。

在这种情况下，不能使用设备，并且计算机没有声音。 任务栏上的扬声器图标标记有一个 X 标记。 选择图标时，会收到以下消息：

> 音频服务未响应。 要使音频正常工作，必须运行 Windows 音频和 Windows 音频终结点生成器服务。

## <a name="cause"></a>原因

之所以出现这种 "音频未播放" 问题，是因为默认的 USB 音频2.0 驱动程序（usbaudio2）使用 WaveRT 端口进行操作，但设备特定的驱动程序并不是这样。 但是，在注册设备接口后，这两个驱动程序都使用 "波形" 引用字符串。
当设备特定的驱动程序替换默认驱动程序时，仍使用 usbaudio2 创建的设备接口，因为引用字符串重叠。 因此，操作系统假定新驱动程序还支持 WaveRT 端口。 由于新的驱动程序不支持 WaveRT 端口，系统无法访问驱动程序。

## <a name="resolution"></a>分辨率

若要解决此问题，请使用以下方法之一。

### <a name="method-1"></a>方法 1

卸载设备。 要实现此目的，请执行下列步骤：

1. 打开“设备管理器”。
1. 右键单击（或点击并按住）设备的名称，然后选择 "**卸载**"。

> 注意：在步骤2中，不要选中 "**删除此设备的驱动程序软件**" 复选框。

### <a name="method-2"></a>Method 2

将设备连接到其他 USB 端口。 如果设备连接到其他 USB 端口，则可能不会出现此问题。

### <a name="method-3"></a>方法3

如果设备尚未连接，请先安装设备特定驱动程序。 为此，可以使用适用于设备的安装程序。 然后，连接设备。 Windows 现在选择特定于设备的驱动程序，而不是默认的 USB 音频2.0 驱动程序。 此方法适用于这种情况，这是因为仅当设备连接后设备特定驱动程序替换默认驱动程序时，才会出现此问题。

## <a name="see-also"></a>另请参阅

[音频设备故障排除](audio-devices-troubleshooting.md)
