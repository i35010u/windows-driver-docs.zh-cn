---
title: 编码器实现和支持
description: 编码器实现和支持
ms.assetid: 6ba97ff8-815b-490f-920b-6ede4f730e98
keywords:
- 编码器设备 WDK AVStream
- AVStream WDK，编码器设备
- 未压缩的数据流 WDK AVStream
- 编码流 WDK AVStream
- 音频编码器设备 WDK AVStream
- 视频编码器设备 WDK AVStream
- 属性集 WDK 编码器
- ENCAPIPARAM_BITRATE_MODE
- ENCAPIPARAM_BITRATE
- ENCAPIPARAM_PEAK_BITRATE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 419e27157c430b0cc90916cb57469b671d7fa167
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192875"
---
# <a name="encoder-implementation-and-support"></a>编码器实现和支持

在 Windows XP Service Pack 1 中，Microsoft 在 *ksmedia* 中定义了三个内核流式处理属性集和一个枚举，以支持仅视频编码器设备。 每个属性集都包含一个属性。 换言之，每个属性都接收其自己的属性集。 如果你的驱动程序进行了*get*属性或*设置*属性调用，则在设置调用时，请在[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)结构的**Set**成员中指定*ksmedia*) 中定义的属性集的 GUID (，并在**Id**成员中指定零：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性 Set</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/encapiparam-bitrate" data-raw-source="[ENCAPIPARAM_BITRATE](./encapiparam-bitrate.md)">ENCAPIPARAM_BITRATE</a></td>
<td><p>实现此属性集可指定编码器设备支持的编码比特率。 有关更多详细信息，请参阅 <a href="encoder-code-examples.md" data-raw-source="[Encoder Code Examples](encoder-code-examples.md)">编码器代码示例</a> 。</p></td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/encapiparam-bitrate-mode" data-raw-source="[ENCAPIPARAM_BITRATE_MODE](./encapiparam-bitrate-mode.md)">ENCAPIPARAM_BITRATE_MODE</a></td>
<td><p>实现此属性集可指定设备支持的编码模式。 此属性集使用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-videoencoder_bitrate_mode" data-raw-source="[&lt;strong&gt;VIDEOENCODER_BITRATE_MODE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-videoencoder_bitrate_mode)"><strong>VIDEOENCODER_BITRATE_MODE</strong></a> 枚举来指定支持的模式。 有关更多详细信息，请参阅 <a href="encoder-code-examples.md" data-raw-source="[Encoder Code Examples](encoder-code-examples.md)">编码器代码示例</a> 。</p></td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/encapiparam-peak-bitrate" data-raw-source="[ENCAPIPARAM_PEAK_BITRATE](./encapiparam-peak-bitrate.md)">ENCAPIPARAM_PEAK_BITRATE</a></td>
<td><p>实现此属性集可指定设备的最大编码比特率。</p></td>
</tr>
</tbody>
</table>

客户端通过从 Windows 软件开发包 (SDK) 文档) 中描述的 " **IEncoderAPI** com (接口" 派生**IVideoEncoder** com 接口，来访问这些属性。

微型驱动程序必须为每个 ENCAPIPARAM Xxx 属性指定默认值 \_ *Xxx* 。 主题 [编码器代码示例](encoder-code-examples.md) 演示如何指定默认属性值。 在开发和调试编码器筛选器的过程中，可以从支持 ENCAPIPARAM \_ 比特率属性集的微型驱动程序触发当前属性页。

在 DirectX 9.0 中，在 *ksmedia* 中定义了六个附加属性集和一个事件集，以更好地支持更多种编码器，包括仅音频编码器。 与 ENCAPIPARAM \_ *Xxx*属性一样，每个属性都接收其自己的属性集：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性 Set</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-video-encoder" data-raw-source="[CODECAPI_VIDEO_ENCODER](./codecapi-video-encoder.md)">CODECAPI_VIDEO_ENCODER</a></td>
<td><p>如果你的设备支持编码视频流 (包括 TV 音频等辅助音频) 则实现对此属性集的支持。</p></td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-audio-encoder" data-raw-source="[CODECAPI_AUDIO_ENCODER](./codecapi-audio-encoder.md)">CODECAPI_AUDIO_ENCODER</a></td>
<td><p>如果设备是仅音频编码器，则实现对此属性集的支持，而不是 CODECAPI_VIDEO_ENCODER。</p></td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-setalldefaults" data-raw-source="[CODECAPI_SETALLDEFAULTS](./codecapi-setalldefaults.md)">CODECAPI_SETALLDEFAULTS</a></td>
<td><p>实现此属性将设置为将所有编码器设备的内部设置（例如，将比特率和编码模式编码为其默认值）。</p></td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-allsettings" data-raw-source="[CODECAPI_ALLSETTINGS](./codecapi-allsettings.md)">CODECAPI_ALLSETTINGS</a></td>
<td><p>实现此属性集以传达编码器设备的当前设置。 此属性集用于与客户端之间的通信。</p></td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-supportsevents" data-raw-source="[CODECAPI_SUPPORTSEVENTS](./codecapi-supportsevents.md)">CODECAPI_SUPPORTSEVENTS</a></td>
<td><p>如果设备支持来自用户模式的事件（例如更改编码模式、比特率或其他设置），则实现此属性集。 如果实现此属性集，则还必须实现对 CODECAPI_CHANGELISTS 事件的支持。</p></td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-currentchangelist" data-raw-source="[CODECAPI_CURRENTCHANGELIST](./codecapi-currentchangelist.md)">CODECAPI_CURRENTCHANGELIST</a></td>
<td><p>实现此属性可设置，以确定先前调用中更改了哪些编码器参数以设置一个或多个编码器属性。</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>事件集</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-changelists" data-raw-source="[CODECAPI_CHANGELISTS](./codecapi-changelists.md)">CODECAPI_CHANGELISTS</a></p></td>
<td><p>如果设备通过 CODECAPI_SUPPORTSEVENTS 属性集支持响应用户模式事件，则实现此事件集可返回编码器设置列表，这些设置是客户端的对 CODECAPI_SETALLDEFAULTS 或 CODECAPI_ALLSETTINGS 的之前的 <em>设置</em>属性调用的结果发生更改。</p></td>
</tr>
</tbody>
</table>

客户端通过 **ICodecAPI** COM 接口访问这些属性 (Windows SDK 文档) 中所述。 有关 COM 接口的详细信息，请参阅 [编码器安装和注册](encoder-installation-and-registration.md) ，其中包括如何指定 KsProxy 应公开的接口。

微型驱动程序应实现对基本 *get*属性查询的支持。 主题 [编码器代码示例](encoder-code-examples.md) 演示如何支持 *获取*-属性查询。

开发编码器筛选器时，将编码功能从视频捕获筛选器移动到单独的筛选器中。 定义自己的专用媒体，使图形生成器能够正确地连接编码器和捕获筛选器。 如果硬件能够控制非编码内容，则可能还会公开公共媒介。 如果同时实现公共和专用媒体，请首先列出专用媒体，因为它可以减少图形构建时间;生成筛选器图时查找正确的筛选器。

若要详细了解如何在单独的筛选器图中使用筛选器的多个筛选器实例 () 参阅 [媒体和类别](mediums-and-categories.md)。