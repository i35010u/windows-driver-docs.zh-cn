---
title: 默认的声音样本集
description: 默认的声音样本集
ms.assetid: 9ffcb7ef-173f-4db9-85e8-2af7eb64cb75
keywords:
- 硬件加速 WDK 音频
- 微型端口驱动程序 WDK 音频，内核模式硬件加速
- 合成器 WDK 音频，内核模式硬件加速
- DirectMusic 内核模式 WDK 音频，默认声音样本集
- 内核模式 synths WDK 音频，默认声音样本集
- 默认声音样本集
- 声音示例会将 WDK 音频设置
- 合成器 WDK 音频，默认的声音设置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b2ac801dd1e954468bd5954968a890921ed2e64
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533103"
---
# <a name="default-sound-sample-sets"></a>默认的声音样本集


## <span id="default_sound_sample_sets"></span><span id="DEFAULT_SOUND_SAMPLE_SETS"></span>


某些合成器附带默认声音集符合 General MIDI 或其中一些扩展。 此声音的集提供的应用程序不支持示例下载，或希望默认声音集下载示例结合使用。 有两种可能的传递机制集声音： 以预先打包的 DLS 集的形式或作为 ROM 集。

在预打包 DLS 集的情况下的一组管理委托给 DirectMusic。 Microsoft 提供了基于 Roland GS 示例的默认 DLS 集。 若要使用不同的默认设置的硬件的制造商应联系 Microsoft DirectMusic 组。 以这种方式提供的示例集不应设置指示一组示例; 的硬件支持的功能位仅 ROM 集应设置这些位。

ROM 集同样由系统管理。 为了通过可下载的示例中保留的内存最大的示例供使用，微型端口驱动程序不应加载到 RAM 的示例设置了整个 ROM。 （这不是可以直接从 rom。 示例的硬件的问题）提供自身的更新更改之前，系统提供所需更新检测的下载请求。 如果检测下载是指在 ROM 示例集中的更新，然后**dwDLId** DMU 成员\_DOWNLOADINFO 结构 （Microsoft Windows SDK 文档中所述） 包含标记下载\_ID\_ROMSET （定义为 0xFFFFFFFF）。

 

 




