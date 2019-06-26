---
title: 语音分配
description: 语音分配
ms.assetid: fb1e6c36-02b4-41a6-b9c4-09f393d389db
keywords:
- DirectMusic 内核模式 WDK 音频，语音分配
- 内核模式 synths WDK 音频，语音分配
- 语音分配 WDK 音频
- 硬件加速 WDK 音频
- 微型端口驱动程序 WDK 音频，内核模式硬件加速
- 合成器 WDK 音频，内核模式硬件加速
- 合成器 WDK 音频，语音分配
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 653566fc7e8bad546fbc33b44f92614bcabadbf8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354134"
---
# <a name="voice-allocation"></a>语音分配


## <span id="voice_allocation"></span><span id="VOICE_ALLOCATION"></span>


大多数适配器驱动程序，包含合成器微型端口驱动程序还包含 DirectSound 硬件加速。 此时将显示语音合成语音和硬件加速 DirectSound 缓冲区之间的分配的问题。

DirectMusic synths-硬件和软件 — 应支持多个实例，以便最大限度的并发客户端数量。 合成器编写器可能会想到以静态方式分配到 synths，语音，但可能应将所有可用实例的 synths 视为绘图中常见的动态语音池。 每个实例然后报告可用的语音数为池中的总数量。

如果实现这种方式，甚至有限数量的物理语音硬件合成支持众多合成器实例。 在真实时间中的统计信息调用通知当前正在使用多少语音每个实例的客户端。 如果动态池耗尽时，合成器实例需要一个新的声音，该合成器实例必须实现以释放该实例中的从语音的语音窃取方案。

以下的分配方案是，语音合成器通过使用更轻松地共享高于 DirectSound 缓冲区因为驱动程序可以控制哪些数据会以何种语音和可以做出有关语音窃取 （DLS 级别中所述的理论基础1 规范）。

所有可用于微型端口驱动程序 （硬件、 软件或硬件和软件的某些组合） 的语音分为两个池。 第一个池，可用池，包含的任何位置不会提交的语音。 第二个池，动态池，包含要使用通过提交合成器实例的语音。 这些语音可能或可能不当前正由合成器实例的使用。 动态池的大小调整为语音合成器的任何实例，受约束的可用池的当前内容请求的最大数目。 DirectSound 缓冲区是从可用池进行分配时移除并返回上释放。

下表包含说明在实践中的方案的语音分配的示例的序列。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Time</th>
<th align="left">请求</th>
<th align="left">可用池</th>
<th align="left">动态池</th>
<th align="left">微型端口驱动程序操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>T0</p></td>
<td align="left"><p>打开电源</p></td>
<td align="left"><p>64</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>初始化。</p></td>
</tr>
<tr class="even">
<td align="left"><p>T1</p></td>
<td align="left">DSound (4)</td>
<td align="left"><p>60</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>以静态方式分配给 DirectSound 缓冲区的四个语音。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>T2</p></td>
<td align="left">合成器 (32)</td>
<td align="left"><p>28</p></td>
<td align="left"><p>32</p></td>
<td align="left"><p>增加到 32 语音动态池。</p></td>
</tr>
<tr class="even">
<td align="left"><p>T3</p></td>
<td align="left">合成 (24)</td>
<td align="left"><p>28</p></td>
<td align="left"><p>32</p></td>
<td align="left"><p>执行任何操作。 在动态池中已存在多个 24 语音。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>T4</p></td>
<td align="left">DSound (24)</td>
<td align="left"><p>4</p></td>
<td align="left"><p>32</p></td>
<td align="left"><p>以静态方式分配给 DirectSound 缓冲区 24 语音。</p></td>
</tr>
<tr class="even">
<td align="left"><p>T5</p></td>
<td align="left">合成 （48 个）</td>
<td align="left"><p>0</p></td>
<td align="left"><p>36</p></td>
<td align="left"><p>增加到 36 语音动态池。 （创建端口的方法，则返回 S_FALSE，并设置 DMUS_PORTPARAMS。<strong>dwVoices</strong> = 36。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>T6</p></td>
<td align="left">DSound (10)</td>
<td align="left"><p>0</p></td>
<td align="left"><p>36</p></td>
<td align="left"><p>失败。 任何种声线中可用池。</p></td>
</tr>
<tr class="even">
<td align="left"><p>T7</p></td>
<td align="left">DSound (-5)</td>
<td align="left"><p>5</p></td>
<td align="left"><p>36</p></td>
<td align="left"><p>免费的五个语音。 请注意，这些不会返回到动态池中，即使最后一个请求 （在时间 T5） 时的详细信息不是授予了。</p></td>
</tr>
</tbody>
</table>

 

请注意，DirectSound 缓冲区实际分配，出于可读性目的表中组合在一起。

立即创建合成器 pin 实例后，应根据其不分配任何语音。 创建过程中后不久, [ **KSPROPERTY\_合成\_PORTPARAMETERS** ](https://docs.microsoft.com/previous-versions/ff537405(v=vs.85))接收到的属性项。 此外，此属性项指示是要与此实例相关联的语音数。 此项目还提供了无法分配有机会在所有请求的语音的情况下报告动态池的实际新大小的微型端口驱动程序。

 

 




