---
title: 默认的声音样本集
description: 默认的声音样本集
keywords:
- 硬件加速 WDK 音频
- 微型端口驱动程序 WDK 音频、内核模式硬件加速
- 合成 WDK 音频，内核模式硬件加速
- DirectMusic 内核模式 WDK 音频，默认声音示例集
- 内核模式 synths WDK 音频，默认声音示例集
- 默认声音示例集
- 声音示例集 WDK 音频
- 合成 WDK 音频，默认声音集
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5916ed8e6ef4897962972d7fa7baadbcd35a652
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789297"
---
# <a name="default-sound-sample-sets"></a>默认的声音样本集


## <span id="default_sound_sample_sets"></span><span id="DEFAULT_SOUND_SAMPLE_SETS"></span>


有些合成程序附带了一个默认的声音集，该声音集符合一般 MIDI 或其中某个扩展。 对于不支持下载示例的应用程序或希望将默认声音设置为与下载的示例一起使用的应用程序，将提供此声音集。 此类声音集有两种可能的交付机制：作为预打包的 DLS 集或 ROM 集。

对于预打包的 DLS 集，该集的管理将委派给 DirectMusic。 Microsoft 提供了一个基于 Roland GS 示例的默认 DLS 集。 希望将不同的默认集用于其硬件的制造商应与 Microsoft 的 DirectMusic 组联系。 以这种方式提供的示例集不应设置指示示例集硬件支持的功能位;只有 ROM 集应该设置这些位。

ROM 集也由系统进行管理。 为了保留可供下载的示例使用的最大内存量，小型端口驱动程序不应将整个 ROM 集加载到示例 RAM 中。  (这不是可以直接在 ROM 外播放样本的硬件问题。 ) 系统在提供更新更改本身之前，为所需的更新提供了检测下载请求。 如果检测下载是指 ROM 示例集中的更新，则 **dwDLId** \_ Microsoft Windows SDK 文档中所述的 dmu DOWNLOADINFO 结构的 dwDLId 成员 (文档中) 包含 \_ 0xffffffff) 定义的标记下载 ID \_ (ROMSET。

 

 




