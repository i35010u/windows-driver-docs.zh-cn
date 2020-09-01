---
title: 语音分配
description: 语音分配
ms.assetid: fb1e6c36-02b4-41a6-b9c4-09f393d389db
keywords:
- DirectMusic 内核模式 WDK 音频，语音分配
- 内核模式 synths WDK 音频，语音分配
- 语音分配 WDK 音频
- 硬件加速 WDK 音频
- 微型端口驱动程序 WDK 音频、内核模式硬件加速
- 合成 WDK 音频，内核模式硬件加速
- 合成 WDK 音频，语音分配
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8bef84b341e326fab675911d6529b77ba1de833
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206663"
---
# <a name="voice-allocation"></a>语音分配


## <span id="voice_allocation"></span><span id="VOICE_ALLOCATION"></span>


大多数包含合成器微型端口驱动程序的适配器驱动程序还包含 DirectSound 硬件加速。 这就提出了合成器语音与硬件加速 DirectSound 缓冲区之间的语音分配问题。

DirectMusic synths--硬件和软件都支持多个实例，以便最大限度地提高并发客户端数量。 合成者可能会尝试将语音静态分配给 synths，但可能会将 synths 的所有可用实例视为来自公共的动态语音池中的绘图。 然后，每个实例都将可用的语音数量报告为池中可用的总数量。

以这种方式实现时，即使有有限数量的物理语音的硬件合成也可以支持大量合成实例。 统计调用会实时向客户端通知每个实例当前所使用的声音数量。 如果动态池已耗尽并且合成实例需要新的语音，则该合成实例必须实现一种语音偷窃方案，以便从该实例中释放语音。

下面的分配方案基于这样一种想法：合成器使用的声音比 DirectSound 缓冲器更易于共享，因为该驱动程序可以控制哪些数据进入什么声音，并可以根据 DLS Level 1 规范) 中概述的语音偷窃 (作出决策。

可用于微型端口驱动程序的所有声音 (硬件、软件或硬件和软件) 的某种组合分为两个池。 第一个池（免费池）包含未在任何位置提交的声音。 第二个池（动态池）包含提交给合成器实例使用的声音。 合成器实例当前可能正在使用或可能未使用这些声音。 动态池的大小为任何合成器实例请求的最大声音数量，受空闲池的当前内容的限制。 DirectSound 缓冲区在分配后将从空闲池中删除，并在释放时返回。

下表包含一系列语音分配示例，用于演示实践方案。

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
<th align="left">时间</th>
<th align="left">请求</th>
<th align="left">可用池</th>
<th align="left">动态池</th>
<th align="left">微型端口驱动程序操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>T0</p></td>
<td align="left"><p>开机</p></td>
<td align="left"><p>64</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>初始化.</p></td>
</tr>
<tr class="even">
<td align="left"><p>T1</p></td>
<td align="left">DSound (4) </td>
<td align="left"><p>60</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>静态分配四个声音到 DirectSound 缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>T2</p></td>
<td align="left">合成 (32) </td>
<td align="left"><p>28</p></td>
<td align="left"><p>32</p></td>
<td align="left"><p>将动态池增加到32声音。</p></td>
</tr>
<tr class="even">
<td align="left"><p>T3</p></td>
<td align="left">合成 (24) </td>
<td align="left"><p>28</p></td>
<td align="left"><p>32</p></td>
<td align="left"><p>不执行任何操作。 动态池中已有超过24个声音。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>T4</p></td>
<td align="left">DSound (24) </td>
<td align="left"><p>4</p></td>
<td align="left"><p>32</p></td>
<td align="left"><p>静态地将24个声音分配给 DirectSound 缓冲区。</p></td>
</tr>
<tr class="even">
<td align="left"><p>T5</p></td>
<td align="left">合成 (48) </td>
<td align="left"><p>0</p></td>
<td align="left"><p>36</p></td>
<td align="left"><p>将动态池增加到36声音。  (创建端口的方法将返回 S_FALSE 并设置 DMUS_PORTPARAMS。<strong>dwVoices</strong> = 36. ) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>T6</p></td>
<td align="left">DSound (10) </td>
<td align="left"><p>0</p></td>
<td align="left"><p>36</p></td>
<td align="left"><p>Fail。 免费池中没有语音。</p></td>
</tr>
<tr class="even">
<td align="left"><p>T7</p></td>
<td align="left">DSound (-5) </td>
<td align="left"><p>5</p></td>
<td align="left"><p>36</p></td>
<td align="left"><p>免费5声。 请注意，这些操作不会回到动态池中，即使) 的最后一个请求 (的时间超过了。</p></td>
</tr>
</tbody>
</table>

 

请注意，DirectSound 缓冲区实际上是逐个分配的，并在表中组合在一起以便于阅读。

一旦创建了合成器 pin 实例，就不应根据它分配任何声音。 创建后不久，会收到 [**KSPROPERTY \_ 合成 \_ PORTPARAMETERS**](/previous-versions/ff537405(v=vs.85)) 属性项。 此属性项指示要与此实例相关联的语音数，以及其他事项。 此项还使微型端口驱动程序能够报告返回动态池的实际新大小，以防无法分配所有请求的声音。

 

