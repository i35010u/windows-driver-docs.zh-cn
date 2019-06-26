---
title: IDirectMusicSynth 和 IDirectMusicSynthSink
description: IDirectMusicSynth 和 IDirectMusicSynthSink
ms.assetid: ce9a353b-9e4b-402b-92bb-948200e3c2ef
keywords:
- IDirectMusicSynth 接口
- IDirectMusicSynthSink 接口
- 自定义呈现在用户模式 WDK 音频中，接口
- 用户模式下 synths WDK 音频，接口
- 自定义批接收器 WDK 音频
- 批接收器 WDK 音频，用户模式
- 延迟 WDK 音频，合成器
- master 时钟 WDK 音频，合成器
- 时钟 WDK 音频，合成器
- 合成器 WDK 音频，接口
- 自定义 synths WDK 音频，接口
- DirectMusic 自定义呈现 WDK 音频，合成器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6473e987c649664bd8f1c29de1fdd4e19ebf43d7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359953"
---
# <a name="idirectmusicsynth-and-idirectmusicsynthsink"></a>IDirectMusicSynth 和 IDirectMusicSynthSink


## <span id="idirectmusicsynth_and_idirectmusicsynthsink"></span><span id="IDIRECTMUSICSYNTH_AND_IDIRECTMUSICSYNTHSINK"></span>


如中所述[合成和批接收器](synthesizers-and-wave-sinks.md)，可以实现自定义软件合成器或批接收器在用户模式下运行，并与 DirectMusic 进行通信。 合成器对象必须具有[IDirectMusicSynth](https://docs.microsoft.com/windows/desktop/api/dmusics/nn-dmusics-idirectmusicsynth)接口。 批接收器对象必须具有[IDirectMusicSynthSink](https://docs.microsoft.com/windows/desktop/api/dmusics/nn-dmusics-idirectmusicsynthsink)接口。

DirectMusic 与软件合成器通过其**IDirectMusicSynth**接口。 DirectMusic 支持此接口中 DirectX 6.1 和更高版本。 **IDirectMusicSynth**支持下表，将方法组织到功能组中所示的方法。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Group</th>
<th align="left">方法名称</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>激活</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-activate" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::Activate&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-activate)"><strong>IDirectMusicSynth::Activate</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>通道</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getchannelpriority" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::GetChannelPriority&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getchannelpriority)"><strong>IDirectMusicSynth::GetChannelPriority</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-setchannelpriority" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::SetChannelPriority&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-setchannelpriority)"><strong>IDirectMusicSynth::SetChannelPriority</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Instruments</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-download" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::Download&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-download)"><strong>IDirectMusicSynth::Download</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-unload" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::Unload&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-unload)"><strong>IDirectMusicSynth::Unload</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>信息</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getappend" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::GetAppend&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getappend)"><strong>IDirectMusicSynth::GetAppend</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getformat" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::GetFormat&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getformat)"><strong>IDirectMusicSynth::GetFormat</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getlatencyclock" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::GetLatencyClock&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getlatencyclock)"><strong>IDirectMusicSynth::GetLatencyClock</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getportcaps" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::GetPortCaps&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getportcaps)"><strong>IDirectMusicSynth::GetPortCaps</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getrunningstats" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::GetRunningStats&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getrunningstats)"><strong>IDirectMusicSynth::GetRunningStats</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>“播放”</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-playbuffer" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::PlayBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-playbuffer)"><strong>IDirectMusicSynth::PlayBuffer</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-render" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::Render&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-render)"><strong>IDirectMusicSynth::Render</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>端口</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-open" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::Open&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-open)"><strong>IDirectMusicSynth::Open</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-close" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::Close&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-close)"><strong>IDirectMusicSynth::Close</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-setnumchannelgroups" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::SetNumChannelGroups&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-setnumchannelgroups)"><strong>IDirectMusicSynth::SetNumChannelGroups</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>其他参数</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-setmasterclock" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::SetMasterClock&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-setmasterclock)"><strong>IDirectMusicSynth::SetMasterClock</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-setsynthsink" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::SetSynthSink&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-setsynthsink)"><strong>IDirectMusicSynth::SetSynthSink</strong></a></p></td>
</tr>
</tbody>
</table>

 

大多数应用程序不需要调用中的方法**IDirectMusicSynth**直接接口; DirectMusic 端口通常管理合成器。 但是，你的应用程序可以直接向合成器接口在开发和测试过程。

合成器未完成而无需与批接收器，这表示为具有的对象的连接**IDirectMusicSynthSink**接口。 批接收器将合成器的音频输出流连接到一个音频呈现模块，如 DirectSound、 DirectShow、 或 Windows 多媒体**waveOut** API。

默认情况下使用其内部 DirectMusic **IDirectMusicSynthSink**实现以处理软件合成器生成的批数据。 此批接收器馈送到 DirectSound 数据。

可以激活合成器之前，批接收器必须首先是创建并连接到通过调用合成**IDirectMusicSynth::SetSynthSink**。 这应该是创建合成器，因为之后的第一次调用的计时相关的调用包括许多**IDirectMusicSynth::GetLatencyClock**和**IDirectMusicSynth::SetMasterClock**，将实际传递到等效的调用**IDirectMusicSynthSink**。

只有 DirectX 6.1 和 DirectX 7 支持的自定义的用户模式下批接收器与实现**IDirectMusicSynthSink**接口。 **IDirectMusicSynthSink**支持下表，将方法组织到功能组中所示的方法。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Group</th>
<th align="left">方法名称</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>初始化</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-activate" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::Activate&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-activate)"><strong>IDirectMusicSynthSink::Activate</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-getdesiredbuffersize" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::GetDesiredBufferSize&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-getdesiredbuffersize)"><strong>IDirectMusicSynthSink::GetDesiredBufferSize</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-init" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::Init&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-init)"><strong>IDirectMusicSynthSink::Init</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-setdirectsound" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::SetDirectSound&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-setdirectsound)"><strong>IDirectMusicSynthSink::SetDirectSound</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>定时</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-getlatencyclock" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::GetLatencyClock&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-getlatencyclock)"><strong>IDirectMusicSynthSink::GetLatencyClock</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-reftimetosample" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::RefTimeToSample&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-reftimetosample)"><strong>IDirectMusicSynthSink::RefTimeToSample</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-sampletoreftime" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::SampleToRefTime&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-sampletoreftime)"><strong>IDirectMusicSynthSink::SampleToRefTime</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-setmasterclock" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::SetMasterClock&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-setmasterclock)"><strong>IDirectMusicSynthSink::SetMasterClock</strong></a></p></td>
</tr>
</tbody>
</table>

 

DirectX 8 及更高版本，DirectMusic 始终使用用户模式下合成器使用其内部批接收器。 DirectMusic 这些更高版本不支持的自定义实现**IDirectMusicSynthSink**。

在 DirectX 6.1 和 DirectX 7 中，但是，你可以自由实施您自己**IDirectMusicSynthSink**对象，并使用它来管理合成器的音频输出流中任何喜欢的方式。 例如，可能会将批数据输送到 DirectShow 或**waveOut** API。 如果您创建的批流对象，它必须具有**IDirectMusicSynthSink**接口以插入**IDirectMusicSynth**对象。

除了管理批流，批接收器负责控制合成器的计时。 批接收器通过调用接收主时钟**IDirectMusicSynth::SetMasterClock**，其中将主时间源传递上的相同调用**IDirectMusicSynthSink::SetMasterClock**。 从作为批流相同的 crystal 不生成主时钟，因为批接收器必须使其保持同步的时钟偏差的补偿。

此外，以便合成可以跟踪的时间正确，它提供了两个调用以从主时钟时间以采样时间，然后重新转换：

-   **IDirectMusicSynthSink::RefTimeToSample**

-   **IDirectMusicSynthSink::SampleToRefTime**

批接收器生成延迟时钟，因为它实际管理示例获取编写通过调用的时间**IDirectMusicSynth::Render**。 当调用 DirectMusic **IDirectMusicSynth::GetLatencyClock** DirectMusic 的端口，它只需转而调用**IDirectMusicSynthSink::GetLatencyClock**。

当首次打开软件合成器时，DirectMusic 为 DMU 提供合成\_PORTPARAMS 结构 （Microsoft Windows SDK 文档中所述），指定的采样速率和音频输出流的通道数。 合成器然后将这些数据转换到标准[ **WAVEFORMATEX** ](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)批接收器调用时传递到批接收器的结构**IDirectMusicSynth::GetFormat**方法。

有关其他信息，请参阅的说明**IDirectMusic**并**IDirectMusicPort** Windows SDK 文档中的接口。

 

 




