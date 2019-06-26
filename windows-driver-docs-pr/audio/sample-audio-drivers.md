---
title: 示例音频驱动程序
description: 示例音频驱动程序
ms.assetid: bea50e70-e1ec-4a66-9bfc-8bd644b07ce7
keywords:
- WDM 音频驱动程序 WDK，示例驱动程序
- 音频驱动程序 WDK，示例驱动程序
- 示例驱动程序 WDK 音频
- Ac97 示例音频驱动程序 WDK 音频
- Dmusuart 示例音频驱动程序 WDK 音频
- Fmsynth 示例音频驱动程序 WDK 音频
- Gfx 示例音频驱动程序 WDK 音频
- Mpu401 示例音频驱动程序 WDK 音频
- Msvad 示例音频驱动程序 WDK 音频
- Sb16 示例音频驱动程序 WDK 音频
- Stdunk 示例音频驱动程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a6fb728afe77ad0c6c4b8aff8c7047c72d56e7f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355272"
---
# <a name="sample-audio-drivers"></a>示例音频驱动程序


## <a name="span-idsysvadaudiosamplespanspan-idsysvadaudiosamplespanspan-idsysvadaudiosamplespansysvad-audio-sample"></a><span id="SYSVAD_Audio_Sample"></span><span id="sysvad_audio_sample"></span><span id="SYSVAD_AUDIO_SAMPLE"></span>SYSVAD 音频示例


**系统虚拟音频设备驱动程序示例 (SYSVAD)**

SYSVAD 驱动程序突出显示了 WDM 音频体系结构的许多重要功能。 这些正在实现可用作一个起始点，编写专有的音频设备的自定义驱动程序的源代码。

*Sysvad*解决方案文件包含以下项目。

-   **TabletAudioSample**

    *TabletAudioSample*项目演示了如何开发 WDM 音频驱动程序公开的多个音频设备的支持。 这些音频设备的某些系统中是嵌入 （扬声器，mic 数组），而有些则是可插入 （耳机演讲者/mic、 蓝牙耳机演讲者/mic）。 驱动程序使用 WaveRT 和呈现设备的音频卸载。 该驱动程序使用而不是实际基于硬件的适配器的"虚拟音频设备"，并突出显示音频卸载 WDM 音频驱动程序体系结构的不同方面。 有关 Windows 音频引擎的详细信息，请参阅[Hardware-Offloaded 音频处理 （Windows 驱动程序）](hardware-offloaded-audio-processing.md)。

-   **PhoneAudioSample**

    *PhoneAudioSample*项目是非常类似于*TabletAudioSample*项目。 它包括针对移动设备的优化。

-   **EndpointsCommon**

    *EndpointsCommon*项目包含到平板电脑和手机的通用代码。 有关详细信息，请参阅[音频的通用 Windows 驱动程序](audio-universal-drivers.md)。

-   **SwapAPO**

    *SwapAPO*项目演示了如何开发音频处理对象。 它包括演示如何注册和注销音频处理对象的示例代码，并还演示了如何自定义控制面板属性页上，以反映中处理对象的可用功能。 有关详细信息，请参阅[Windows 音频处理对象](windows-audio-processing-objects.md)。

-   **KeywordDetectorAdapter**

    *KeywordDetectorAdapter*项目演示了如何开发关键字检测程序适配器。 有关详细信息，请参阅[语音激活](voice-activation.md)。

**下载并从 GitHub 提取 Sysvad 音频示例**

SYSVAD 音频示例位于[Windows 驱动程序示例 GitHub](https://github.com/Microsoft/Windows-driver-samples)。

您可以浏览 Sysvad 音频此处的示例：

<https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad>

请按照下列步骤以下载并打开 SYSVAD 示例。

a. 可以使用 GitHub 工具以使用这些示例。 此外可以下载一个 zip 文件中的通用驱动程序示例。

<https://github.com/Microsoft/Windows-driver-samples/archive/master.zip>

b. Master.zip 文件下载到本地硬盘。

c. 右键单击*Windows 驱动程序示例 master.zip*，然后选择**全部提取**。 指定新文件夹，或浏览到一个现有将存储提取的文件。 例如，可以指定*c:\\DriverSamples\\* 作为新文件将被提取到其中的文件夹。

d. 提取文件后，导航到以下子文件夹。

*C:\\DriverSamples\\音频\\Sysvad*

**在 Visual Studio 中打开驱动程序解决方案**

在 Microsoft Visual Studio 中，单击**文件** &gt; **打开** &gt; **项目/解决方案...** 并导航到包含所提取的文件的文件夹 (例如， *c:\\DriverSamples\\音频\\Sysvad*)。 双击*Sysvad*解决方案文件以将其打开。

在 Visual Studio 中找到解决方案资源管理器。 (如果尚未打开，请将此选择**解决方案资源管理器**从**视图**菜单。)在解决方案资源管理器，可以看到一个具有六个项目的解决方案。

## <a name="span-idsampleaudiodriversspanspan-idsampleaudiodriversspanarchived-audio-samples"></a><span id="sample_audio_drivers"></span><span id="SAMPLE_AUDIO_DRIVERS"></span>已存档的音频示例


这些音频示例支持早期版本的 Microsoft Windows Driver Kit (WDK)。 这些信息可作为 zip 文件下载可用的一部分[此处](https://go.microsoft.com/fwlink/p/?LinkId=618052)。

-   **Microsoft 虚拟音频设备驱动程序示例 (Msvad)**

-   **AC97 Driver (Ac97)**

-   **DirectMusic UART 驱动程序示例 (Dmusuart)**

-   **DirectMusic 软件合成器示例 (ddksynth)**

-   **FM 合成器 (Fmsynth)**

-   **音频适配器示例**

**音频处理编解码器示例**

-   **Msfilter 示例编解码器 (MsFilter)**

-   **Msgsm610 示例编解码器 (gsm610)**

有关详细信息，请参阅随附在 WDK 中的这些示例的自述文件文档。

有关 WDK 示例的信息，请参阅[Windows 驱动程序工具包示例包 （Windows 驱动程序）。](https://docs.microsoft.com/windows-hardware/drivers/samples/index)

 

 




