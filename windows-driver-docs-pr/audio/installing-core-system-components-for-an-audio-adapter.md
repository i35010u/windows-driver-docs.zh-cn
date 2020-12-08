---
title: 为音频适配器安装核心系统组件
description: 为音频适配器安装核心系统组件
keywords:
- 音频适配器 WDK，系统组件
- 适配器驱动程序 WDK 音频，系统组件
- 端口类音频适配器 WDK，系统组件
ms.date: 10/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fbaec00b812f5f63b99c1c0bf3e64f604be193c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799243"
---
# <a name="installing-core-system-components-for-an-audio-adapter"></a>为音频适配器安装核心系统组件


## <span id="installing_core_system_components_for_an_audio_adapter"></span><span id="INSTALLING_CORE_SYSTEM_COMPONENTS_FOR_AN_AUDIO_ADAPTER"></span>


本部分包括有关安装端口类音频适配器的核心系统组件的以下主题：

[在 Windows 中安装](installing-in-windows.md)

在制造商的 "**模型**" 部分中指定的每个硬件 ID 的 " [**INF DDInstall" 部分**](../install/inf-ddinstall-section.md)应指定是否包含 **KS。** WDMAUDIO 中的注册部分。 **WDMAUDIO.Registration** Wdmaudio 中的注册部分。 Ks 文件安装核心内核流式处理组件。 Wdmaudio 文件安装核心 WDM 音频组件。 供应商不应修改或替换这些系统 INF 文件。

 

