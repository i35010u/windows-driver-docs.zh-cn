---
title: 软件卷控制支持
description: 软件卷控制支持
ms.assetid: 2bdc7d01-9e47-4deb-b551-13e9cbc9c844
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25d2fad43f553c9168788ba98341b8fad7389573
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548318"
---
# <a name="software-volume-control-support"></a>软件卷控制支持


在 Windows Vista 及更高版本，不包括的音频硬件和使用关联的物理卷控件放大器提供软件卷支持。

下图显示了 Windows 软件卷支持的简化表示形式。

![说明 windows vista 软件卷的关系图支持 ](images/audio-volume-architecture.png)

该图显示两个单独的音频数据路径。 一个放大器时存在，另一个使用 Windows APO 软件音量控制时。 如果放大器存在，该驱动程序播发，KSPROPERTY\_音频\_VOLUMELEVEL。 如果音频驱动程序并不表示它支持 KSPROPERTY\_音频\_VOLUMELEVEL，Windows 音频引擎就会创建软件音量控制 APO。

在典型的 PC 上，只有一个这些数据路径将会显示，因为通常将一组计算机中的音频组件。 用于说明目的，这里显示了两个路径。

[ **IAudioEndpointVolume** ](https://msdn.microsoft.com/library/windows/desktop/dd370892)接口表示音频流上的音量控制到或从音频终结点设备。

如果存在 Bluetooth 打印机或 USB 音频，则将单独控制其音量控件。

## <a name="span-iddatapathwithamplifierpresentspanspan-iddatapathwithamplifierpresentspanspan-iddatapathwithamplifierpresentspandata-path-with-amplifier-present"></a><span id="Data_path_with_amplifier_present"></span><span id="data_path_with_amplifier_present"></span><span id="DATA_PATH_WITH_AMPLIFIER_PRESENT"></span>使用放大器存在的数据路径


当客户端应用程序调用[ **IAudioEndpointVolume** ](https://msdn.microsoft.com/library/windows/desktop/dd370892)在配置中没有放大器并且存在的一个物理卷控件，音频驱动程序公开 KSNODETYPE接口\_卷节点拓扑筛选器中。 卷节点的存在使得**IAudioEndpointVolume**识别的音频信号的卷级别将被修改的硬件。

## <a name="span-iddatapathwithnoamplifierpresentspanspan-iddatapathwithnoamplifierpresentspanspan-iddatapathwithnoamplifierpresentspandata-path-with-no-amplifier-present"></a><span id="Data_path_with_no_amplifier_present"></span><span id="data_path_with_no_amplifier_present"></span><span id="DATA_PATH_WITH_NO_AMPLIFIER_PRESENT"></span>与任何放大器存在的数据路径


当存在，没有放大器[ **IAudioEndpointVolume** ](https://msdn.microsoft.com/library/windows/desktop/dd370892)适用于音频引擎初始化 Windows 软件卷支持 APO。

由于没有任何物理卷控件进行建模，KSNODETYPE\_拓扑筛选器中未公开的卷节点。 卷衰减并获得由 APO 软件卷支持组件执行。

有关卷范围和不同版本的 Windows 默认卷级别的信息，请参阅[默认音频音量设置](default-audio-volume-settings.md)。

 

 




