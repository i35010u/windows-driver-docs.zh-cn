---
title: IDirectMusicSynth 和 IDirectMusicSynthSink
description: IDirectMusicSynth 和 IDirectMusicSynthSink
ms.assetid: ce9a353b-9e4b-402b-92bb-948200e3c2ef
keywords:
- IDirectMusicSynth 接口
- IDirectMusicSynthSink 接口
- 用户模式下的自定义呈现 WDK 音频，接口
- 用户模式 synths WDK 音频，接口
- 自定义波形接收器 WDK 音频
- 波形接收器音频，用户模式
- 延迟 WDK 音频，合成
- 主时钟 WDK 音频，合成
- 时钟 WDK 音频，合成合成
- 合成 WDK 音频，接口
- 自定义 synths WDK 音频，接口
- DirectMusic 自定义呈现 WDK 音频，合成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5d8e3b3cb02f3034755baacb36051144ef7699a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209149"
---
# <a name="idirectmusicsynth-and-idirectmusicsynthsink"></a>IDirectMusicSynth 和 IDirectMusicSynthSink


## <span id="idirectmusicsynth_and_idirectmusicsynthsink"></span><span id="IDIRECTMUSICSYNTH_AND_IDIRECTMUSICSYNTHSINK"></span>


如 "合成器" [和 "波形接收器](synthesizers-and-wave-sinks.md)" 中所述，可以实现在用户模式下运行的自定义软件合成器或波形接收器，并与 DirectMusic 进行通信。 合成器对象必须具有 [IDirectMusicSynth](/windows/desktop/api/dmusics/nn-dmusics-idirectmusicsynth) 接口。 波形接收器对象必须具有 [IDirectMusicSynthSink](/windows/desktop/api/dmusics/nn-dmusics-idirectmusicsynthsink) 接口。

DirectMusic 通过其 **IDirectMusicSynth** 接口与软件合成器通信。 DirectMusic 在 DirectX 6.1 和更高版本中支持此接口。 **IDirectMusicSynth** 支持下表中显示的方法，这些方法将方法组织到功能组中。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">组</th>
<th align="left">方法名称</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>激活</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-activate" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::Activate&lt;/strong&gt;](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-activate)"><strong>IDirectMusicSynth：： Activate</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>信道</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getchannelpriority" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::GetChannelPriority&lt;/strong&gt;](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getchannelpriority)"><strong>IDirectMusicSynth::GetChannelPriority</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-setchannelpriority" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::SetChannelPriority&lt;/strong&gt;](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-setchannelpriority)"><strong>IDirectMusicSynth::SetChannelPriority</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>乐器</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-download" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::Download&lt;/strong&gt;](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-download)"><strong>IDirectMusicSynth：:D o) </strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-unload" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::Unload&lt;/strong&gt;](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-unload)"><strong>IDirectMusicSynth：： Unload</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>信息</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getappend" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::GetAppend&lt;/strong&gt;](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getappend)"><strong>IDirectMusicSynth::GetAppend</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getformat" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::GetFormat&lt;/strong&gt;](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getformat)"><strong>IDirectMusicSynth：： Iformatprovider.getformat</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getlatencyclock" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::GetLatencyClock&lt;/strong&gt;](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getlatencyclock)"><strong>IDirectMusicSynth::GetLatencyClock</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getportcaps" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::GetPortCaps&lt;/strong&gt;](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getportcaps)"><strong>IDirectMusicSynth::GetPortCaps</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getrunningstats" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::GetRunningStats&lt;/strong&gt;](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-getrunningstats)"><strong>IDirectMusicSynth::GetRunningStats</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>播放</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-playbuffer" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::PlayBuffer&lt;/strong&gt;](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-playbuffer)"><strong>IDirectMusicSynth：:P layBuffer</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-render" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::Render&lt;/strong&gt;](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-render)"><strong>IDirectMusicSynth：： Render</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>端口</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-open" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::Open&lt;/strong&gt;](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-open)"><strong>IDirectMusicSynth：： Open</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-close" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::Close&lt;/strong&gt;](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-close)"><strong>IDirectMusicSynth：： Close</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-setnumchannelgroups" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::SetNumChannelGroups&lt;/strong&gt;](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-setnumchannelgroups)"><strong>IDirectMusicSynth::SetNumChannelGroups</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>其他参数</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-setmasterclock" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::SetMasterClock&lt;/strong&gt;](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-setmasterclock)"><strong>IDirectMusicSynth::SetMasterClock</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-setsynthsink" data-raw-source="[&lt;strong&gt;IDirectMusicSynth::SetSynthSink&lt;/strong&gt;](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-setsynthsink)"><strong>IDirectMusicSynth::SetSynthSink</strong></a></p></td>
</tr>
</tbody>
</table>

 

大多数应用程序不需要直接调用 **IDirectMusicSynth** 接口中的方法;DirectMusic 端口通常管理合成器。 但是，你的应用程序可以在开发和测试过程中直接向合成器进行接口。

无需连接到波形接收器即可完成合成器，这种方式表示为具有 **IDirectMusicSynthSink** 接口的对象。 波形接收器将合成器的音频输出流连接到音频渲染模块，如 DirectSound、DirectShow 或 Windows 多媒体 **waveOut** API。

默认情况下，DirectMusic 使用其内部 **IDirectMusicSynthSink** 实现来处理软件合成器生成的波形数据。 此波形接收器将数据馈送到 DirectSound。

在可以激活合成器之前，必须先通过调用 **IDirectMusicSynth：： SetSynthSink**来创建和连接到合成器。 这应该是创建合成器后的第一次调用，因为许多与计时相关的调用（包括 **IDirectMusicSynth：： GetLatencyClock** 和 **IDirectMusicSynth：： SetMasterClock**）实际上都传递到 **IDirectMusicSynthSink**上的等效调用。

仅 DirectX 6.1 和 DirectX 7 支持通过 **IDirectMusicSynthSink** 接口实现自定义用户模式波形接收器。 **IDirectMusicSynthSink** 支持下表中显示的方法，这些方法将方法组织到功能组中。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">组</th>
<th align="left">方法名称</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>初始化</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-activate" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::Activate&lt;/strong&gt;](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-activate)"><strong>IDirectMusicSynthSink：： Activate</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-getdesiredbuffersize" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::GetDesiredBufferSize&lt;/strong&gt;](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-getdesiredbuffersize)"><strong>IDirectMusicSynthSink::GetDesiredBufferSize</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-init" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::Init&lt;/strong&gt;](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-init)"><strong>IDirectMusicSynthSink：： Init</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-setdirectsound" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::SetDirectSound&lt;/strong&gt;](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-setdirectsound)"><strong>IDirectMusicSynthSink::SetDirectSound</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>定时</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-getlatencyclock" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::GetLatencyClock&lt;/strong&gt;](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-getlatencyclock)"><strong>IDirectMusicSynthSink::GetLatencyClock</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-reftimetosample" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::RefTimeToSample&lt;/strong&gt;](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-reftimetosample)"><strong>IDirectMusicSynthSink::RefTimeToSample</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-sampletoreftime" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::SampleToRefTime&lt;/strong&gt;](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-sampletoreftime)"><strong>IDirectMusicSynthSink::SampleToRefTime</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-setmasterclock" data-raw-source="[&lt;strong&gt;IDirectMusicSynthSink::SetMasterClock&lt;/strong&gt;](/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-setmasterclock)"><strong>IDirectMusicSynthSink::SetMasterClock</strong></a></p></td>
</tr>
</tbody>
</table>

 

在 DirectX 8 及更高版本中，DirectMusic 始终将其内部波形接收器与用户模式合成器一起使用。 这些更高版本的 DirectMusic 不支持 **IDirectMusicSynthSink**的自定义实现。

不过，在 DirectX 6.1 和 DirectX 7 中，你可以自由地实现自己的 **IDirectMusicSynthSink** 对象，并使用它来按你喜欢的任何方式管理合成器的音频输出流。 例如，可能会将波形数据送入 DirectShow 或 **waveOut** API。 如果创建波形流对象，则该对象必须具有 **IDirectMusicSynthSink** 接口，才能插入 **IDirectMusicSynth** 对象。

除了管理波形流外，波形接收器还负责控制合成器的计时。 波形接收器通过调用 **IDirectMusicSynth：： SetMasterClock**接收主时钟，后者通过对 **IDirectMusicSynthSink：： SetMasterClock**的相同调用传递上的主时间源。 因为主时钟不是从与波形流相同的 crystal 生成的，所以波形接收器必须通过补偿时钟偏移使它们保持同步。

另外，为了使合成器可以持续跟踪时间，它提供了两个调用以将主时钟时间转换为采样时间，并返回回来：

-   **IDirectMusicSynthSink::RefTimeToSample**

-   **IDirectMusicSynthSink::SampleToRefTime**

波形接收器会生成延迟时钟，因为它实际上管理通过调用 **IDirectMusicSynth：： Render**写入样本的时间。 当 DirectMusic 调用 DirectMusic 端口上的 **IDirectMusicSynth：： GetLatencyClock** 时，它只需转到 **IDirectMusicSynthSink：： GetLatencyClock**即可。

首次打开软件合成器时，DirectMusic 将为合成器提供一个 DMU \_ PORTPARAMS 结构 Microsoft Windows SDK () 指定音频输出流的采样速率和通道数。 然后，合成器将它们转换为标准的 [**WAVEFORMATEX**](/windows/desktop/api/mmreg/ns-mmreg-twaveformatex) 结构，当波形接收器调用 **IDirectMusicSynth：： iformatprovider.getformat** 方法时，它会传递给波形接收器。

有关其他信息，请参阅 Windows SDK 文档中的 **IDirectMusic** 和 **IDirectMusicPort** 接口的说明。

 

