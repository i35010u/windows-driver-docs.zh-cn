---
title: 探索 Windows Vista 音频引擎
description: 探索 Windows Vista 音频引擎
ms.assetid: 6301f6d7-57f5-4b9f-9567-57efb9dc58f3
ms.date: 11/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: b7dd26437fba19251729fe31dc9a8b92a4564465
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333710"
---
# <a name="exploring-the-windows-vista-audio-engine"></a>探索 Windows Vista 音频引擎


本主题概述了 Windows Vista 音频引擎。 它主要关注将帮助你了解 a p o s 和 sAPOs 如何协同工作的概念。

下图显示了简化的布局的音频引擎的内部结构。

![说明 windows vista 音频的关系图引擎简化的布局](images/sysfxapo-custom-details.png)

与关系图所示，系统提供 a p o s 和 sAPOs 是音频引擎的基本构建基块。 音频引擎配置为调用管道的组件的系统提供 a p o s 和 sAPOs。 有两种类型的音频引擎中的管道：

-   Stream 管道由 a p o s 和 sAPOs 执行数字音频处理本地到流从一个应用程序的组成。 在这种类型的管道 sAPO 称为本地效果 sAPO (LFX sAPO)。

-   设备管道由 a p o s 和执行全局影响的所有流的数字音频处理 sAPOs 组成。 在这种类型的管道 sAPO 称为全局效果 sAPO (GFX sAPO)。

下表显示了 sAPOs 所提供的 Windows Vista 音频引擎和系统效果它们所应用的类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows Vista sAPO</th>
<th align="left">系统效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>低音增强</p></td>
<td align="left"><p>LFX</p></td>
</tr>
<tr class="even">
<td align="left"><p>低音管理</p></td>
<td align="left"><p>LFX</p></td>
</tr>
<tr class="odd">
<td align="left"><p>响度均衡</p></td>
<td align="left"><p>LFX</p></td>
</tr>
<tr class="even">
<td align="left"><p>低频保护</p></td>
<td align="left"><p>LFX</p></td>
</tr>
<tr class="odd">
<td align="left"><p>扬声器填充</p></td>
<td align="left"><p>LFX</p></td>
</tr>
<tr class="even">
<td align="left"><p>扬声器构成幻路</p></td>
<td align="left"><p>LFX</p></td>
</tr>
<tr class="odd">
<td align="left"><p>虚拟环绕</p></td>
<td align="left"><p>LFX</p></td>
</tr>
<tr class="even">
<td align="left"><p>虚拟化通过耳机的外侧代码</p></td>
<td align="left"><p>LFX</p></td>
</tr>
<tr class="odd">
<td align="left"><p>增强的便携式计算机声音</p></td>
<td align="left"><p>GFX</p></td>
</tr>
<tr class="even">
<td align="left"><p>房间修正</p></td>
<td align="left"><p>GFX</p></td>
</tr>
</tbody>
</table>

 

当音频应用程序启动音频处理时，音频引擎配置系统提供不和 sAPOs 化为音频图形处理数字音频数据。 用于生成音频图形的音频引擎使用该机制是系统的详细信息，不作介绍。

音频应用程序可以启动在共享的模式或排他模式连接。 一组默认的 sAPOs 安装了 Windows Vista，尽管 sAPOs 不被视为是系统组件，因此可自定义。

### <a name="span-idsharedmodespanspan-idsharedmodespanshared-mode"></a><span id="shared_mode"></span><span id="SHARED_MODE"></span>共享模式

在共享模式下，音频应用程序与其他进程中运行其他音频应用程序共享的音频硬件。 音频引擎将混合流来自这些应用程序，并播放通过硬件生成的组合。 在共享模式下打开一个流的任何应用程序必须选择音频引擎使用的混合格式。 使用共享模式的优点是，Windows Vista 音频引擎提供了内置音频处理对象 (APO) 来提供所需的支持功能。 使用共享模式的缺点是音频流延迟较高，比处于独占模式。 下面的代码示例显示了用于初始化在共享模式下的音频流的语法。

```cpp
 hResult = pAudioClient->Initialize(
        AUDCLNT_SHAREMODE_SHARED, 
        0,
        0,
        0,
 pWfx,
        &m_SubmixGuid);
```

### <a name="span-idexclusivemodespanspan-idexclusivemodespanexclusive-mode"></a><span id="exclusive_mode"></span><span id="EXCLUSIVE_MODE"></span>排他模式

与此相反，当应用程序独占模式下打开流，该应用程序的音频硬件对独占访问权限。 在此模式下应用程序可以选择任何终结点支持的音频格式。 使用排他模式的优点是音频流延迟低于处于共享模式。 使用独占模式下的缺点是，你必须提供你自己 APO 来处理的音频引擎支持的功能。 只有少量的专业级别的应用程序需要此操作模式。 下面的代码示例显示了用于初始化排他模式中的音频流的语法。

```cpp
 hResult = pAudioClient->Initialize(
            AUDCLNT_SHAREMODE_EXCLUSIVE,
            0,
            0,
            0,  
 pWfxEx,
            &m_SubmixGuid);
```

应用程序启动音频处理后，图形生成器 sAPOs 配置到音频图形，还可以初始化 sAPOs。 与 LFX sAPO 建立音频数据的输入和输出 sAPO 格式然后协商音频服务。 有关详细信息，请参阅[格式协商](format-negotiation.md)。

 

 




