---
title: 探索 Windows Vista 音频引擎
description: 探索 Windows Vista 音频引擎
ms.date: 11/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: fbd682e4db2dce7b76f5d30d170f6e186184fde0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784833"
---
# <a name="exploring-the-windows-vista-audio-engine"></a>探索 Windows Vista 音频引擎


本主题提供 Windows Vista 音频引擎的概述。 其中重点介绍了有助于您了解如何和 sAPOs 一起工作的概念。

下图显示了音频引擎内部结构的简化布局。

![演示 windows vista 音频引擎简化布局的示意图](images/sysfxapo-custom-details.png)

如图所示，系统提供的中和 sAPOs 是音频引擎的基本构建基块。 音频引擎将系统提供的 "中" 和 "sAPOs" 配置到称为管道的组件中。 音频引擎中有两种类型的管道：

-   流管道由 "中" 和 "sAPOs" 组成，它们执行从单个应用程序到流的本地数字音频处理。 此类管道中的 sAPO 称为本地效果 sAPO (LFX sAPO) 。

-   设备管道由 "中" 和 "sAPOs" 组成，用于执行数字音频处理，该处理会影响所有流的全局效果。 此类管道中的 sAPO 称为全局效果 sAPO (GFX sAPO) 。

下表显示了 Windows Vista 音频引擎中可用的 sAPOs 以及它们适用的系统效果类型。

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
<td align="left"><p>虚拟化环绕耳机</p></td>
<td align="left"><p>LFX</p></td>
</tr>
<tr class="odd">
<td align="left"><p>便携计算机的增强型声音</p></td>
<td align="left"><p>GFX</p></td>
</tr>
<tr class="even">
<td align="left"><p>房间修正</p></td>
<td align="left"><p>GFX</p></td>
</tr>
</tbody>
</table>

 

当音频应用程序启动音频处理时，音频引擎会将系统提供的 "sAPOs" 和 "" 配置为音频图形，以处理数字音频数据。 音频引擎用于生成音频图形的机制是系统详细信息，不会对其进行讨论。

音频应用程序可以以共享模式或独占模式启动连接。 尽管使用 Windows Vista 安装了一组默认的 sAPOs，但不会将 sAPOs 视为系统组件，因此可对其进行自定义。

### <a name="span-idshared_modespanspan-idshared_modespanshared-mode"></a><span id="shared_mode"></span><span id="SHARED_MODE"></span>共享模式

在共享模式下，音频应用程序与其他进程中运行的其他音频应用程序共享音频硬件。 音频引擎混合了这些应用程序的流，并通过硬件播放产生的组合。 任何在 "共享" 模式下打开流的应用程序都必须选择音频引擎所使用的混合格式。 使用共享模式的优点在于，Windows Vista 音频引擎提供内置的音频处理对象 (APO) 提供必要的支持功能。 使用共享模式的缺点是音频流延迟高于独占模式。 下面的代码示例演示了在共享模式下初始化音频流的语法。

```cpp
 hResult = pAudioClient->Initialize(
        AUDCLNT_SHAREMODE_SHARED, 
        0,
        0,
        0,
 pWfx,
        &m_SubmixGuid);
```

### <a name="span-idexclusive_modespanspan-idexclusive_modespanexclusive-mode"></a><span id="exclusive_mode"></span><span id="EXCLUSIVE_MODE"></span>独占模式

相反，当应用程序在独占模式下打开流时，应用程序具有对音频硬件的独占访问权限。 在此模式下，应用程序可以选择终结点支持的任何音频格式。 使用独占模式的优点是：音频流延迟低于共享模式。 使用独占模式的缺点是必须提供自己的 APO 来处理音频引擎的支持功能。 只有少量的专业级应用程序需要此操作模式。 下面的代码示例演示了在独占模式下初始化音频流的语法。

```cpp
 hResult = pAudioClient->Initialize(
            AUDCLNT_SHAREMODE_EXCLUSIVE,
            0,
            0,
            0,  
 pWfxEx,
            &m_SubmixGuid);
```

在应用程序启动音频处理后，图形生成器将 sAPOs 配置为音频图形并初始化 sAPOs。 然后，音频服务与 LFX sAPO 协商，以便在 sAPO 的输入和输出中建立音频数据的格式。 有关详细信息，请参阅 [格式协商](format-negotiation.md)。

 

 




