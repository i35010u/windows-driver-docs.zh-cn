---
title: AEC 系统筛选器
description: AEC 系统筛选器
ms.assetid: 45865e8c-7080-428f-b436-6004a8d5c011
keywords:
- 回声抵消乐曲音频
- AEC WDK 音频
- NS WDK 音频
- 干扰声音频
- 数据格式化 WDK 音频，AEC 系统筛选器
- 呈现输出音响音频
- 捕获输出音响音频
- 呈现器引脚音频
- 捕获-pin 音响音频
- 筛选 WDK 音频，AEC 系统筛选器
- 连接 WDK 音频
- 筛选器图形 WDK 音频，AEC 系统筛选器
- 音频筛选器曲线图 WDK
ms.date: 11/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: d98d122597f5758c56bba60eace51a995394257b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208387"
---
# <a name="aec-system-filter"></a>AEC 系统筛选器


## <span id="aec_system_filter"></span><span id="AEC_SYSTEM_FILTER"></span>


AEC 系统筛选器 ( # A0) 在软件中 (AEC) 和干扰阻止 (NS) 算法实现声音回声取消。 此筛选器是 Windows XP 和更高版本中的标准操作系统组件。 有关 DirectSoundCapture 应用程序如何允许使用 AEC 系统筛选器的信息，请参阅 Microsoft Windows SDK 文档。

### <a name="span-idconstraints_imposed_by_aec_system_filterspanspan-idconstraints_imposed_by_aec_system_filterspanspan-idconstraints_imposed_by_aec_system_filterspanconstraints-imposed-by-aec-system-filter"></a><span id="Constraints_Imposed_by_AEC_System_Filter"></span><span id="constraints_imposed_by_aec_system_filter"></span><span id="CONSTRAINTS_IMPOSED_BY_AEC_SYSTEM_FILTER"></span>AEC 系统筛选器施加的约束

包含在 AEC 系统筛选器中实现的捕获效果的音频筛选器图受到以下限制：

-   AEC 系统筛选器只能连接到处理 PCM 数据格式的 pin。

-   对于捕获流，位深度必须为16位，而呈现流的位深度必须是8或16位。

-   AEC 系统筛选器以 16 kHz 执行所有内部处理。 输入流和输出流是根据需要进行转换的源速率。

-   在 Windows XP SP1、Windows Server 2003 和更高版本中，AEC 系统筛选器的捕获和呈现器 pin (参阅下图) 必须具有相同的采样率，但可以独立于其他 pin 选择每个传入和向外插针的采样速率。 捕获插针的采样速率可以 (按首选项) 16 kHz、48 kHz、44.1 kHz 或 8 kHz 的顺序进行。  (首选项的顺序取决于处理时间和音频质量。 ) 可以按首选项) 16 kHz、48 kHz 或 44.1 kHz 的顺序 (输出的采样速率。 请注意，该呈现器 pin 不支持采样速率 8 kHz。

![阐释 aec 系统筛选器的 pin 和连接的关系图](images/aecfilt.png)

-   AEC 和 NS 节点 (参见显示 [硬件加速捕获效果](exposing-hardware-accelerated-capture-effects.md) 的图) 只能处理 monophonic 流。 如果捕获流是多通道 (例如两通道立体声) ，则将忽略第一个通道以外的所有通道 (并丢弃) 。 呈现端只能处理 monophonic 流。

-   在 Windows XP SP1、Windows Server 2003 及更高版本中，此限制不存在。 AEC 系统筛选器会正确地处理捕获和呈现流的时钟之间的不匹配，并且可以使用单独的设备来捕获和呈现。

-   使用 AEC 系统筛选器时， [SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver) 将关闭硬件加速以实现混合、采样率转换、3d spatialization 等。 所有流混合都是通过 [KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)在软件仿真中完成的。 此限制是必需的，以确保可通过 AEC 系统筛选器从捕获流中取消呈现设备播放的所有音频。

-   在关系图的捕获端上或在呈现端的 aec 或 ns 节点之后的任何信号处理过程中，或者在呈现端的 AEC 或 NS 节点之后，必须是固定的。 在这些位置的任何一个位置执行任何非线性或时间变化的信号处理可防止 AEC 取消捕获信号中的回声。

-   AEC 筛选仅取消来自您的计算机中由 AEC 筛选的通道的回显。 通过不通过 AEC 的通道输出的音频不会取消回声。 非 AEC 音频通道中的回声在功能上相当于在您的计算机旁边的办公室中的收音机上播放的音频中的回声。 AEC 无法取消 (，而且不会对来自无线电或非 AEC 通道的) 回声产生任何影响。

上述要求适用于所有内核流式传输音频筛选器图形，其中包含在 Aec.sys 中实现的捕获效果。 这些限制反映了如何设计和实现 AEC 系统筛选器的基本假设。 流格式的约束可能会在将来的 Windows 版本中发生更改。

使用 AEC 系统筛选器的任何产品设计都应考虑前面的约束。 以下问题和解答说明了这些约束如何影响 AEC 筛选行为：

问：我已经创建了一个用于立体声呈现的 DirectSound 缓冲区，但在使用 AEC 时，这两个信道的声音都是相同的。 为什么会这样？

答： AEC 仅适用于 mono 流，因此 KMixer 将立体声流混合回 mono 以满足此约束。

问：当我使用 AEC 时，为什么我的 44 kHz，16位音频声音（如 16 kHz）？

答：因为 AEC 系统筛选器以 16 kHz 执行所有内部处理。

问：为什么无法使用 AEC 获取硬件加速的 DirectSound 缓冲区？

答：因为当启用 AEC 时，SysAudio 会关闭硬件加速混合。

问： AEC 系统筛选器是否会与我的旧声霸卡16卡一起使用？

答：是的。 虽然 Sound Blaster16 卡无法同时管理16位呈现和捕获流，但它可以同时管理8位呈现流和16位捕获流，这是一个与 AEC 系统筛选器的输出和捕获支持的组合。 新的音频卡应该设计为至少支持16位的位深度，同时呈现和捕获。

### <a name="span-idsummary_of_data_formats_for_aec_pinsspanspan-idsummary_of_data_formats_for_aec_pinsspanspan-idsummary_of_data_formats_for_aec_pinsspansummary-of-data-formats-for-aec-pins"></a><span id="Summary_of_Data_Formats_for_AEC_Pins"></span><span id="summary_of_data_formats_for_aec_pins"></span><span id="SUMMARY_OF_DATA_FORMATS_FOR_AEC_PINS"></span>AEC Pin 的数据格式摘要

启用 AEC 系统筛选器的 DirectSound 应用程序可以为其 DirectSound 缓冲区选择 KMixer 支持的任何采样率或样本大小。 KMixer 在进入 AEC 系统筛选器之前，将数据从应用程序的呈现缓冲区转换为 16 kHz 的单色16位格式。 同样，在离开 AEC 系统筛选器后，KMixer 可以将目标为 DirectSoundCapture 应用程序捕获缓冲区的数据转换为 16 kHz 单色16位格式。 但是，若要最大程度地减少在图形中完成的处理量并获得最高的音频质量，应用程序应使用 16-kHz 的单色16位格式来呈现和捕获缓冲区。

如果你想要音频硬件使用 AEC 系统筛选器，则硬件呈现 pin 必须至少支持一个 AEC 呈现器 pin 支持的采样速率，而硬件捕获 pin 必须支持 AEC 捕获-传入 pin 支持的采样速率之一。 若要获得最佳的 AEC 性能，你的硬件应支持 16 kHz 采样率以及它所支持的任何更高的费率。 通过支持 16 kHz 速率，硬件减少了无需执行采样率转换，从而减少了 AEC 系统筛选器必须执行的处理量。

AEC 系统筛选器的呈现器 pin 连接到 KMixer 的输出插针。 KMixer 将其输入流的必要转换为呈现输入的 pin 所需的格式。 呈现器 pin 仅支持两种数据格式：

-   大小为16位的 16 kHz mono PCM 格式

-   大小为8位的 16 kHz mono PCM 格式

捕获 pin 仅支持一种格式：

-   大小为16位的 16 kHz mono PCM 格式

如果 DirectSoundCapture 应用程序的缓冲区格式为 16-kHz 单声道16位 PCM，则可以绕过 KMixer 并直接连接到 DSound.DLL (参阅前面的图) 。 否则，AEC 捕获输出会连接到 KMixer，这会将 16 kHz mono 16 位 PCM 流从 pin 转换为应用程序的捕获缓冲区使用的任何格式。

AEC 呈现器输出可处理以下任意格式：

-   具有两个通道的 16 kHz 16 位 PCM (立体声) 

-   具有两个通道的 16 kHz 8 位 PCM

-   含两个通道的 48-kHz 16 位 PCM

-   含两个通道的 48-kHz 8 位 PCM

-   含两个通道的 44.1-kHz 16 位 PCM

-   含两个通道的 44.1-kHz 8 位 PCM

呈现器 pin 通过将单个通道从 AEC 节点复制到输出流的两个通道，生成一个立体声流。

捕获传入 pin 可以处理以下任意格式：

-   带有任意数量通道的 16 kHz 16 位 PCM

-   带有任意数量通道的 48-kHz 16 位 PCM

-   带有任意数量通道的 44.1-kHz 16 位 PCM

-   8 kHz 16 位 PCM，具有任意数量的通道

捕获到 pin 仅使用第一个通道，忽略 (，并放弃其他通道) 。

所有 AEC 系统筛选器的 pin 均使用下表中显示的数据格式参数值。

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

 

有关 **MajorFormat**、 **SubFormat**和 **说明符** 成员的详细信息，请参阅 [**KSDATARANGE**](/previous-versions/ff561658(v=vs.85))。 有关使用这三个参数值的 [**KSDATARANGE \_ 音频**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio) 数据范围描述符的示例，请参阅 [PCM Stream data range](pcm-stream-data-range.md)。

 

