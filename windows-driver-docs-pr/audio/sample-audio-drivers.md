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
ms.openlocfilehash: c56894fad537af5328a4a1857e0f180d7d6d0e8b
ms.sourcegitcommit: f610410e1500f0b0a4ca008b52679688ab51033d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252901"
---
# <a name="sample-audio-drivers"></a>示例音频驱动程序


## <a name="span-idsysvad_audio_samplespanspan-idsysvad_audio_samplespanspan-idsysvad_audio_samplespansysvad-audio-sample"></a><span id="SYSVAD_Audio_Sample"></span><span id="sysvad_audio_sample"></span><span id="SYSVAD_AUDIO_SAMPLE"></span>SYSVAD 音频示例


**系统虚拟音频设备驱动程序示例 (SYSVAD) **

SYSVAD 驱动程序重点介绍了 WDM 音频体系结构的许多重要功能。 这些是使用源代码的工作实现，它们可作为为专有音频设备编写自定义驱动程序的起点。

*Sysvad*解决方案文件包含以下项目。

-   **TabletAudioSample**

    *TabletAudioSample*项目演示了如何开发公开支持多个音频设备的 WDM 音频驱动程序。 其中某些音频设备嵌入 (扬声器、麦克风阵列) 在系统中，而其他音频设备可插 (耳机扬声器/麦克风、蓝牙耳机扬声器/麦克风) 。 驱动程序为呈现设备使用 WaveRT 和音频卸载。 驱动程序使用 "虚拟音频设备" 而不是基于硬件的实际适配器，突出显示音频卸载 WDM 音频驱动程序体系结构的不同方面。 有关 Windows 音频引擎的详细信息，请参阅 [硬件卸载音频处理 (Windows 驱动程序) ](hardware-offloaded-audio-processing.md)。

-   **PhoneAudioSample**

    *PhoneAudioSample*项目与*TabletAudioSample*项目非常相似。 它包括移动设备的优化。

-   **EndpointsCommon**

    *EndpointsCommon*项目包含平板电脑和手机的通用代码。 有关详细信息，请参阅 [适用于音频的通用 Windows 驱动程序](audio-universal-drivers.md)。

-   **SwapAPO**

    *SwapAPO*项目演示了如何开发音频处理对象。 它包括演示如何注册和注销音频处理对象的示例代码，还演示了如何自定义 "控制面板" 属性页以反映处理对象中的可用功能。 有关详细信息，请参阅 [Windows 音频处理对象](windows-audio-processing-objects.md)。

-   **KeywordDetectorAdapter**

    *KeywordDetectorAdapter*项目演示如何开发关键字检测器适配器。 有关详细信息，请参阅 [语音激活](voice-activation.md)。

**从 GitHub 下载并提取 Sysvad 音频示例**

[Windows 驱动程序示例 GitHub](https://github.com/Microsoft/Windows-driver-samples)上提供了 SYSVAD 音频示例。

可在此处浏览 Sysvad 音频示例：

<https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad>

按照以下步骤下载并打开 "SYSVAD" 示例。

a. 您可以使用 GitHub 工具来处理示例。 你还可以将通用驱动程序示例下载到一个 zip 文件中。

<https://github.com/Microsoft/Windows-driver-samples/archive/master.zip>

b. 将 master.zip 文件下载到本地硬盘驱动器。

c. 选择并按住 (或右键单击) *Windows-driver-samples-master.zip*，然后选择 " **全部提取**"。 指定一个新文件夹，或浏览到将存储所提取文件的现有文件夹。 例如，可以指定*C： \\ DriverSamples \\ *作为要将文件提取到的新文件夹。

d. 提取文件后，导航到以下子文件夹。

*C： \\ DriverSamples \\ 音频 \\ Sysvad*

**在 Visual Studio 中打开驱动程序解决方案**

在 Microsoft Visual Studio 中，选择 " **文件**" " &gt; **打开** &gt; **项目/解决方案 ...** "，然后导航到包含所提取文件的文件夹 (例如， *C： \\ DriverSamples \\ Audio \\ Sysvad*) 。 双击 " *Sysvad* " 解决方案文件以将其打开。

在 Visual Studio 中找到解决方案资源管理器。  (如果尚未打开，则从 "**视图**" 菜单中选择 "**解决方案资源管理器**"。 ) 解决方案资源管理器中，你可以看到一个包含六个项目的解决方案。

## <a name="span-idsample_audio_driversspanspan-idsample_audio_driversspanarchived-audio-samples"></a><span id="sample_audio_drivers"></span><span id="SAMPLE_AUDIO_DRIVERS"></span>存档的音频示例


这些音频示例支持以前版本的 Microsoft Windows 驱动程序工具包 (WDK) 。 它们作为 [zip 文件下载](https://github.com/microsoftarchive/msdn-code-gallery-microsoft/tree/master/Official%20Windows%20Driver%20Kit%20Sample/Windows%20Driver%20Kit%20(WDK)%208.1%20Samples)的一部分提供。

-   **Microsoft 虚拟音频设备驱动程序示例 (Msvad) **

-   **AC97 驱动程序 (Ac97) **

-   **DirectMusic UART 驱动程序示例 (Dmusuart) **

-   **DirectMusic 软件合成器示例 (ddksynth) **

-   **FM 合成器 (Fmsynth) **

-   **音频适配器示例**

**音频处理编解码器示例**

-   **Msfilter 示例编解码器 (MsFilter) **

-   **Msgsm610 示例编解码器 (gsm610) **

有关详细信息，请参阅 WDK 中每个示例随附的自述文档。

有关 WDK 示例的信息，请参阅 [Windows 驱动程序工具包示例 Pack (Windows 驱动程序) 。](https://docs.microsoft.com/windows-hardware/drivers/samples/index)

 

 




