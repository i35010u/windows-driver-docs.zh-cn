---
title: AEC 系统筛选器
description: AEC 系统筛选器
ms.assetid: 45865e8c-7080-428f-b436-6004a8d5c011
keywords:
- 回声取消 WDK 音频
- AEC WDK 音频
- NS WDK 音频
- 干扰抑制 WDK 音频
- 数据格式以 WDK 音频，AEC 系统筛选器
- 呈现出插针 WDK 音频
- 捕获扩展插针 WDK 音频
- 呈现器中的 pin WDK 音频
- 捕获在 pin WDK 音频
- 筛选器 WDK 音频，AEC 系统筛选器
- 连接 WDK 音频
- 筛选器关系图 WDK 音频，AEC 系统筛选器
- 音频筛选器关系图 WDK
ms.date: 11/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8ce62b73ba99f467017bb4007ecb5335e438da2e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326019"
---
# <a name="aec-system-filter"></a>AEC 系统筛选器


## <span id="aec_system_filter"></span><span id="AEC_SYSTEM_FILTER"></span>


AEC 系统筛选器 (Aec.sys) 在软件中实现的回声抵消 (AEC) 和干扰抑制 (NS) 算法。 此筛选器是标准的操作系统组件在 Windows XP 及更高版本。 有关如何启用 DirectSoundCapture 应用程序的信息使用 AEC 系统筛选器，请参阅 Microsoft Windows SDK 文档。

### <a name="span-idconstraintsimposedbyaecsystemfilterspanspan-idconstraintsimposedbyaecsystemfilterspanspan-idconstraintsimposedbyaecsystemfilterspanconstraints-imposed-by-aec-system-filter"></a><span id="Constraints_Imposed_by_AEC_System_Filter"></span><span id="constraints_imposed_by_aec_system_filter"></span><span id="CONSTRAINTS_IMPOSED_BY_AEC_SYSTEM_FILTER"></span>约束规定 AEC 系统筛选器

音频筛选器关系图，其中包含在 AEC 系统筛选器中实现一个捕获效果受到以下限制：

-   AEC 系统筛选器只能连接到操作处理 PCM 数据格式的 pin。

-   位深度必须是 16 位用于捕获流和呈现流的 8 或 16 位。

-   AEC 系统筛选器执行所有内部处理在 16 kHz。 输入和输出流是根据需要转换的源的速率。

-   在 Windows XP SP1 中，Windows Server 2003，及更高版本，AEC 系统筛选器捕获扩展和呈现在插针 （请参阅下图） 必须具有相同的采样率，但在捕获中并呈现出插针的采样率可以每个选择独立于其他 pin。 16 kHz、 48khz、 44.1 kHz 或 8 kHz 采样率在捕获中 pin 可以 （按优先顺序）。 （首选项的顺序取决于处理时间和音频质量。）采样率在呈现出 pin 可以是 （按优先顺序） 16 kHz、 48khz 或 44.1 kHz。 请注意，呈现出 pin 不支持 8 kHz 采样率。

![说明 aec 系统筛选器的插针和连接的关系图](images/aecfilt.png)

-   AEC 和 NS 节点 (请参阅第一个图[Exposing Hardware-Accelerated 捕获效果](exposing-hardware-accelerated-capture-effects.md)) 可以处理仅单声道流。 如果捕获流是多渠道 （例如，两个通道立体声），第一个以外的所有通道将被忽略 （并丢弃）。 仅单声道流可由呈现端处理。

-   在 Windows XP SP1 中，Windows Server 2003，及更高版本，不存在此限制。 AEC 系统正确筛选捕获的时钟之间的句柄不匹配，并将呈现流，并单独的设备可用于捕获和呈现。

-   当使用 AEC 系统筛选器时， [SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)关闭硬件加速的混合、 采样率转换、 3D spatialization 等。 流的所有混合使用所示通过软件仿真[KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)。 此限制是需要确保捕获流外 AEC 系统筛选器，可以取消所有呈现设备，将会播放的音频。

-   任何信号处理程序完成后再捕获端关系图的 AEC 前后的 AEC 或 NS 节点或呈现器端 NS 节点必须是线性的时间不变。 执行任何非线性或时间改变的信号处理在以下位置会阻止 AEC 取消捕获信号中的回显。

-   AEC 筛选取消只回显来自您的计算机中的 AEC 筛选通道。 音频，它是通过不通过 AEC 的渠道的输出未取消 echo。 在非 AEC 音频通道中的回显是功能上等效于在办公室中相邻计算机广播播放音频中回显。 AEC 具有从单选或非 AEC 通道没有取消 （和不会影响） 的方法回显。

上述要求适用于所有内核流音频筛选器图形，其中融合了捕获在 Aec.sys 中实现的效果。 这些限制反映的设计和实现的 AEC 系统筛选器中的基本假设。 流格式的约束可能会更改在将来的版本的 Windows。

使用 AEC 系统筛选器的任何产品设计应考虑到上述约束。 以下问题和答案显示这些约束如何影响 AEC 筛选行为：

问:我创建了立体声呈现 DirectSound 缓冲区，但这两个通道听起来相同，当我使用 AEC。 这是为什么？

答：因此 KMixer 混合使用立体声流返回到 mono 以满足此约束，仅对 mono 流起作用的 AEC。

问:为什么 does 我 44 kHz、 16 位音频听起来像 16 kHz 时我使用 AEC？

答：因为 AEC 系统筛选器执行所有内部处理在 16 kHz。

问:为什么不能获取使用 AEC 的硬件加速 DirectSound 缓冲区？

答：因为 SysAudio 会关闭 AEC 启用硬件加速混合使用。

问:AEC 系统筛选器会使用我的旧声音 Blaster 16 卡？

答：是。 尽管声音 Blaster16 卡不能同时管理 16 位呈现和捕获流，但它可以同时管理的 8 位呈现流和 16 位捕获流是组合的 AEC 系统筛选器的呈现扩展和支持捕获中的 pin。 音频的新卡片应旨在支持至少 16 位的位深度的呈现和捕获。

### <a name="span-idsummaryofdataformatsforaecpinsspanspan-idsummaryofdataformatsforaecpinsspanspan-idsummaryofdataformatsforaecpinsspansummary-of-data-formats-for-aec-pins"></a><span id="Summary_of_Data_Formats_for_AEC_Pins"></span><span id="summary_of_data_formats_for_aec_pins"></span><span id="SUMMARY_OF_DATA_FORMATS_FOR_AEC_PINS"></span>摘要数据格式以获得 AEC 的 Pin

任何采样率或 KMixer 支持的示例大小，DirectSound 应用程序，AEC 系统筛选器可以选择针对其 DirectSound 缓冲区。 进入 AEC 系统筛选器之前，KMixer 将数据从应用程序的呈现缓冲区转换为 16 kHz mono 16 位格式。 同样，KMixer 可以转换在离开 AEC 系统筛选器之后为 16 kHz mono 16 位格式 DirectSoundCapture 应用程序的捕获缓冲区发送到的数据。 但是，若要同时最大程度减少在关系图中完成的处理量和实现最高的音频质量，应用程序应使用 16 kHz mono 16 位格式的呈现和捕获缓冲区。

如果您希望您的音频硬件以处理 AEC 系统筛选器，则硬件呈现 pin 必须至少一个支持的 AEC 呈现出 pin 的采样率和支持硬件捕获 pin 必须支持下述某个支持的 AEC capt 采样速率在此中的 pin。 若要实现最佳的 AEC 性能，您的硬件应支持任何更高的速率，它支持除了一个 16 kHz 采样率。 通过支持 16 kHz 速率，硬件可减少处理 AEC 系统筛选器必须执行操作，无需执行采样率转换量。

AEC 系统筛选器的呈现器在插针连接到 KMixer 的输出插针。 KMixer 执行必要的转换其输入流的呈现器在 pin 要求的格式。 呈现在 pin 支持只有两种数据格式：

-   16-kHz mono PCM 格式使用 16 位样本大小

-   16-kHz mono PCM 格式使用样本大小为 8 位

捕获扩展 pin 支持仅一种格式：

-   16-kHz mono PCM 格式使用 16 位样本大小

如果 DirectSoundCapture 应用程序的缓冲区格式是 16 kHz mono 的 16 位 PCM，AEC 捕获扩展 pin 可以绕过 KMixer，直接连接到 DSound.DLL （参见前面的图）。 否则，AEC 捕获扩展插针连接到 KMixer，转换为 16 kHz mono 16 位 PCM 流 pin 任何格式的应用程序捕获缓冲区使用。

AEC 呈现出 pin 可以处理任一以下格式：

-   包含两条通道 （立体声） 16 kHz 16 位 PCM

-   包含两条通道 16 kHz 8 位 PCM

-   使用两个通道的 48 kHz 16 位 PCM

-   使用两个通道的 48 kHz 8 位 PCM

-   包含两条通道 44.1 kHz 16 位 PCM

-   包含两条通道 44.1 kHz 8 位 PCM

呈现扩展 pin 生成的立体声流通过将单个通道从 AEC 节点复制到输出流的两个通道。

捕获在 pin 可以处理任一以下格式：

-   使用任意数目的信道的 16 kHz 16 位 PCM

-   使用任意数目的信道的 48 kHz 16 位 PCM

-   使用任意数目的信道的 44.1 kHz 16 位 PCM

-   使用任意数量的通道 8 kHz 16 位 PCM

捕获在 pin 使用仅第一个通道并将忽略 （和放弃） 其他。

所有的 AEC 系统筛选器的 pin 使用下表中显示的数据格式参数值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">KSDATARANGE 成员</th>
<th align="left">参数值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>MajorFormat</strong></p></td>
<td align="left"><p>KSDATAFORMAT_TYPE_AUDIO</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SubFormat</strong></p></td>
<td align="left"><p>KSDATAFORMAT_SUBTYPE_PCM</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>说明符</strong></p></td>
<td align="left"><p>KSDATAFORMAT_SPECIFIER_WAVEFORMATEX</p></td>
</tr>
</tbody>
</table>

 

有关详细信息**MajorFormat**，**子格式**，并**说明符**成员，请参阅[ **KSDATARANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff561658). 有关的示例[ **KSDATARANGE\_音频**](https://msdn.microsoft.com/library/windows/hardware/ff537096)数据范围说明符，它使用这三个参数值，请参阅[PCM Stream 数据范围](pcm-stream-data-range.md)。

 

 




