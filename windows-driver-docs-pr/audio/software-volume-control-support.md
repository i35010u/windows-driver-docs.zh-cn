---
title: 软件音量控制支持
description: 软件音量控制支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3a12bd520b61c5e7ebb9b8dbb11a1c388b078c4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800665"
---
# <a name="software-volume-control-support"></a>软件音量控制支持


在 Windows Vista 和更高版本中，为不包含关联的物理卷控件并带有放大器的音频硬件提供软件卷支持。

下图显示了 Windows 软件卷支持的简化表示形式。

![说明 windows vista 软件卷支持的示意图 ](images/audio-volume-architecture.png)

此关系图显示了两个单独的音频数据路径。 一种情况是，当存在一个放大器时，当使用 Windows APO 软件卷控件时，会使用一个。 如果有放大器，驱动程序会公布，KSPROPERTY \_ 音频 \_ VOLUMELEVEL。 如果音频驱动程序未指明它支持 KSPROPERTY \_ 音频 \_ VOLUMELEVEL，则 Windows 音频引擎将创建软件卷控制 APO。

在典型的 PC 上，只会出现其中一个数据路径，因为计算机中通常会有一组音频组件。 此处显示了这两个路径用于说明目的。

[**IAudioEndpointVolume**](/windows/win32/api/endpointvolume/nn-endpointvolume-iaudioendpointvolume)接口表示音频流上音频流中的音量控件和音频终结点设备。

如果存在蓝牙或 USB 音频，则会单独控制其音量控制。

## <a name="span-iddata_path_with_amplifier_presentspanspan-iddata_path_with_amplifier_presentspanspan-iddata_path_with_amplifier_presentspandata-path-with-amplifier-present"></a><span id="Data_path_with_amplifier_present"></span><span id="data_path_with_amplifier_present"></span><span id="DATA_PATH_WITH_AMPLIFIER_PRESENT"></span>具有放大器的数据路径存在


当客户端应用程序在具有放大器且存在物理音量控制的配置中调用 [**IAudioEndpointVolume**](/windows/win32/api/endpointvolume/nn-endpointvolume-iaudioendpointvolume) 接口时，音频驱动程序会 \_ 在拓扑筛选器中公开一个 KSNODETYPE 卷节点。 卷节点的存在使 **IAudioEndpointVolume** 知道音频信号的音量级别将由硬件修改。

## <a name="span-iddata_path_with_no_amplifier_presentspanspan-iddata_path_with_no_amplifier_presentspanspan-iddata_path_with_no_amplifier_presentspandata-path-with-no-amplifier-present"></a><span id="Data_path_with_no_amplifier_present"></span><span id="data_path_with_no_amplifier_present"></span><span id="DATA_PATH_WITH_NO_AMPLIFIER_PRESENT"></span>不存在放大器的数据路径


如果不存在放大器， [**IAudioEndpointVolume**](/windows/win32/api/endpointvolume/nn-endpointvolume-iaudioendpointvolume) 将与音频引擎配合使用来初始化 Windows 软件卷支持 APO。

由于没有要建模的物理卷控制，因此 \_ 拓扑筛选器中不会公开 KSNODETYPE 卷节点。 卷衰减和收益由 APO 软件容量支持组件执行。

有关不同版本的 Windows 的卷范围和默认卷级别的信息，请参阅 [默认音频音量设置](default-audio-volume-settings.md)。

 

