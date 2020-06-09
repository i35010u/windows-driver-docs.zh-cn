---
title: Windows 10 音频驱动程序的新增功能
description: 本主题提供有关 Windows 10 的音频新增功能的高级摘要。
ms.assetid: 9005966A-CCC2-478C-9221-56007B7FADFB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 690b278052dd2c46a558208d8961a4f4eaa913be
ms.sourcegitcommit: 8097a09d2f989a9b3dca250c4e2ffd4cec2172e3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84563153"
---
# <a name="windows-10-whats-new-for-audio-drivers"></a>Windows 10：音频驱动程序的新增功能


本主题提供有关 Windows 10 的音频新增功能的高级摘要。

## <a name="span-idfeature_summaryspanspan-idfeature_summaryspanspan-idfeature_summaryspanfeature-summary"></a><span id="Feature_Summary"></span><span id="feature_summary"></span><span id="FEATURE_SUMMARY"></span>功能摘要


下面是 Windows 10 中新增的音频功能。

-   [实现音频模块通信](implementing-audio-module-communication.md)

-   [低延迟音频改进](#lowlatency)

-   [信号处理模式和音频类别](#signalprocessing)

-   [硬件卸载 APO 效果](#hardwareoffloaded)

-   [Cortana 语音激活](#cortanavoice)

-   [适用于音频的 Windows 通用驱动程序](#windowsuniversal)

-   [音频驱动程序的资源管理](#resourcemanagement)

-   [用于音频驱动程序的 PNP 重新平衡](#pnprebalance)

## <a name="span-idlowlatencyspanspan-idlowlatencyspanspan-idlowlatencyspanlow-latency-audio-improvements"></a><span id="LowLatency"></span><span id="lowlatency"></span><span id="LOWLATENCY"></span>低延迟音频改进


音频延迟是指在该时间内创建声音和听到声音的延迟时间。 对于几个关键方案（如下所示），具有较低的音频延迟非常重要。

-   Pro 音频
-   音乐创建和混合
-   Skype 等通信
-   虚拟和增强的现实
-   游戏

设备的总延迟是以下组件的延迟的总和：

-   操作系统
-   音频处理对象
-   音频驱动程序
-   音频硬件

在 Windows 10 中，执行此操作是为了降低 OS 中的延迟。 如果没有任何驱动程序更改，Windows 10 中的应用程序将遇到 4.5 m32-16ms 的低延迟。 此外，如果驱动程序已更新为利用使用小型缓冲区处理音频数据的新低延迟 DDIs，则延迟将更多。 如果驱动程序支持3ms 音频缓冲区，则往返延迟为 ~ 10ms。

![显示应用、音频引擎驱动程序和 h/w 的低延迟音频堆栈关系图](images/low-latency-audio-stack-diagram-1.png)

音频堆栈支持多个数据包大小和动态数据包大小调整，以便根据用户的情况在延迟和电源之间进行权衡。 此外，流将按优先顺序排列，以确保高优先级流（例如电话呼叫）具有专用资源。

为了使音频驱动程序支持低延迟，Windows 10 提供了以下三个新功能：

1. \[必需 \] 声明每个模式所支持的最小缓冲区大小。
2. \[可选，但建议 \] 改善驱动程序和操作系统之间数据流的协调。
3. \[可选，但建议 \] 注册驱动程序资源（中断、线程），以便它们可以在低延迟方案中受操作系统保护。
有关详细信息，请参阅[低延迟音频](low-latency-audio.md)。

## <a name="span-idsignalprocessingspanspan-idsignalprocessingspanspan-idsignalprocessingspansignal-processing-modes-and-audio-categories"></a><span id="SignalProcessing"></span><span id="signalprocessing"></span><span id="SIGNALPROCESSING"></span>信号处理模式和音频类别


**信号处理模式**

驱动程序声明每个设备支持的音频信号处理模式。

音频类别（由应用程序选择）映射到音频模式（由驱动程序定义）。 Windows 定义了七种音频信号处理模式。 Oem 和 Ihv 可以确定要实现的模式。 下表汇总了这些模式。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><strong>模式</strong></td>
<td align="left"><strong>呈现/捕获</strong></td>
<td align="left"><strong>说明</strong></td>
</tr>
<tr class="even">
<td align="left">Raw</td>
<td align="left">两者</td>
<td align="left"><p>Raw 模式指定不应对流应用任何信号处理。</p>
<p>应用程序可以请求完全不动并执行其自己的信号处理的原始流。</p></td>
</tr>
<tr class="odd">
<td align="left">默认</td>
<td align="left">两者</td>
<td align="left"><p>此模式定义默认音频处理。</p></td>
</tr>
<tr class="even">
<td align="left">部</td>
<td align="left">呈现</td>
<td align="left">电影音频播放</td>
</tr>
<tr class="odd">
<td align="left">许可证</td>
<td align="left">两者</td>
<td align="left">音乐音频播放（大多数媒体流的默认值）</td>
</tr>
<tr class="even">
<td align="left">语速</td>
<td align="left">捕获</td>
<td align="left">人类语音捕获（例如 Cortana 的输入）</td>
</tr>
<tr class="odd">
<td align="left">联系</td>
<td align="left">两者</td>
<td align="left">VOIP 呈现和捕获（例如 Skype、Lync）</td>
</tr>
<tr class="even">
<td align="left">提醒</td>
<td align="left">呈现</td>
<td align="left">铃声、警报、警报等。</td>
</tr>
</tbody>
</table>

 

音频设备驱动程序需要至少支持 Raw 模式或默认模式。 支持附加模式是可选的。

用于语音、电影、音乐和通信的专用模式。 音频驱动程序将能够根据流类型定义不同类型的音频格式和处理。

**音频类别**

下表显示了 Windows 10 中的音频类别。

为了通知系统有关音频流的使用情况，应用程序可以选择使用特定的音频流类别标记流。 在 Windows 10 中，有九个音频流类别。

|                |                                                                                                       |
|----------------|-------------------------------------------------------------------------------------------------------|
| **类别**   | **说明**                                                                                       |
| 电影\*        | 电影，带对话框的视频（替换 ForegroundOnlyMedia）                                              |
| 媒体\*        | 媒体播放的默认类别（替换 BackgroundCapableMedia）                                 |
| 游戏聊天\*    | 用户之间的游戏间通信（Windows 10 中的新类别）                                      |
| 语音\*       | 语音输入（例如，个人助手）和输出（例如，导航应用）（Windows 10 中的新类别） |
| 通信 | VOIP，实时聊天                                                                                  |
| 警报         | 警报，响铃音，通知                                                                       |
| 声音效果  | 嘟嘟声、dings 等                                                                                     |
| 游戏媒体     | 游戏音乐                                                                                         |
| 游戏效果   | 球弹跳，车载声音，项目符号，等等。                                                      |
| 其他          | 未分类的流                                                                                 |

 

\*Windows 10 中的新增项。

有关详细信息，请参阅[音频信号处理模式](audio-signal-processing-modes.md)和[音频处理对象体系结构](audio-processing-object-architecture.md)。

## <a name="span-idhardwareoffloadedspanspan-idhardwareoffloadedspanspan-idhardwareoffloadedspanhardware-offloaded-apo-effects"></a><span id="HardwareOffloaded"></span><span id="hardwareoffloaded"></span><span id="HARDWAREOFFLOADED"></span>硬件卸载 APO 效果


Windows 10 支持硬件卸载的 APO 效果。 可以加载到卸载 pin 的顶部。 这允许在软件和硬件中进行音频处理。 此外，处理可以动态更改。 当 DSP 中的负载增加时，可以将部分或全部处理从软件 APO 移到 DSP，然后再移回到软件 APO。

有关详细信息，请参阅[实现硬件卸载的 APO 效果](implementing-hardware-offloaded-apo-effects.md)。

## <a name="span-idcortanavoicespanspan-idcortanavoicespanspan-idcortanavoicespancortana-voice-activation---wake-on-voice"></a><span id="CortanaVoice"></span><span id="cortanavoice"></span><span id="CORTANAVOICE"></span>Cortana 语音激活-语音唤醒

Cortana，个人助手技术最初 demonstarted 于2013的 Microsoft BUILD 开发人员大会。 语音激活是一项功能，使用户能够通过口述特定短语 "你好 Cortana" 从各种设备电源状态调用语音识别引擎。 使用 "你好 Cortana" 语音激活（VA）功能，用户可以通过语音在活动上下文之外（即，当前在屏幕上）快速参与体验（例如，Cortana）。 当屏幕关闭、空闲或处于完全活动状态时，该功能将针对方案。 如果硬件支持缓冲，则用户可以将关键短语和命令短语一起链接在一起。 这可以提高用户的端到端唤醒体验。 有关详细信息，请参阅[语音激活](voice-activation.md)。

## <a name="span-idwindowsuniversalspanspan-idwindowsuniversalspanspan-idwindowsuniversalspanwindows-universal-drivers-for-audio"></a><span id="WindowsUniversal"></span><span id="windowsuniversal"></span><span id="WINDOWSUNIVERSAL"></span>适用于音频的 Windows 通用驱动程序


Windows 10 支持适用于 PC 的一个驱动程序模型，2：1个适用于手机和小屏幕平板电脑的 Windows 10。 这意味着 Ihv 可以在一个平台上开发其驱动程序，并且该驱动程序在所有设备（台式机、笔记本电脑、平板电脑和手机）中工作。 这样就缩短了开发时间和成本。

若要开发通用音频驱动程序，请使用以下工具：

1. Visual Studio 2015：新的驱动程序设置允许将 "目标平台" 设置为 "通用" 以创建多平台驱动程序。
2. APIValidator：这是一个 WDK 工具，用于检查驱动程序是否是通用的，并突出显示需要更新的调用。
3. GitHub 中的音频示例： sysvad 和 SwapAPO 已转换为通用驱动程序。
有关详细信息和 GitHub 示例代码的指针，请参阅[适用于音频的通用 Windows 驱动程序](audio-universal-drivers.md)。

## <a name="span-idresourcemanagementspanspan-idresourcemanagementspanspan-idresourcemanagementspanresource-management-for-audio-drivers"></a><span id="ResourceManagement"></span><span id="resourcemanagement"></span><span id="RESOURCEMANAGEMENT"></span>音频驱动程序的资源管理


在成本较低的移动设备上创建良好的音频体验的一个挑战是，某些设备有多种并发约束。 例如，设备可能只能同时播放最多6个音频流，且仅支持2个卸载流。 如果移动设备上存在活动电话呼叫，则设备可能仅支持2个音频流。 当设备正在捕获音频时，设备只能播放最多4个音频流。

Windows 10 包含一种机制，用于表达并发约束，以确保高优先级的音频流和移动电话呼叫能够播放。 如果系统资源不足，则终止低优先级流。 此机制仅适用于不在台式机或笔记本电脑上的手机和平板电脑。

有关详细信息，请参阅[音频硬件资源管理](audio-hardware-resource-management.md)。

## <a name="span-idpnprebalancespanspan-idpnprebalancespanspan-idpnprebalancespanpnp-rebalance-for-audio-drivers"></a><span id="PNPRebalance"></span><span id="pnprebalance"></span><span id="PNPREBALANCE"></span>用于音频驱动程序的 PNP 重新平衡


对于需要重新分配内存资源的某些 PCI 方案，将使用 PNP 重新平衡。 在这种情况下，将卸载某些驱动程序，然后在不同的内存位置重新加载这些驱动程序，以便创建可用的连续内存空间。 可在两种主要方案中触发重新平衡：

1. PCI 热插拔：用户插入设备，PCI 总线没有足够的资源来加载新设备的驱动程序。 属于此类别的设备的一些示例包括闪电、USB-C 和 NVME 存储。 在这种情况下，需要重新排列和合并内存资源（重新平衡）以支持添加的其他设备。
2. PCI resizeable 竖线：在内存中成功加载设备的驱动程序后，它会请求其他资源。 设备的一些示例包括高端图形卡和存储设备。
有关详细信息，请参阅[实现 PortCls 音频驱动程序的 PnP 再平衡](implement-pnp-rebalance-for-portcls-audio-drivers.md)。

 

 




