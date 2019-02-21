---
title: 为音频适配器安装核心系统组件
description: 为音频适配器安装核心系统组件
ms.assetid: fc14867e-cae8-4381-bcd3-ec2230050cf6
keywords:
- 音频适配器 WDK、 系统组件
- 适配器驱动程序 WDK 音频，系统组件
- 端口类音频适配器 WDK、 系统组件
ms.date: 10/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cd1926add0c99bbf1a248997910a75f7ee10440
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522130"
---
# <a name="installing-core-system-components-for-an-audio-adapter"></a>为音频适配器安装核心系统组件


## <span id="installing_core_system_components_for_an_audio_adapter"></span><span id="INSTALLING_CORE_SYSTEM_COMPONENTS_FOR_AN_AUDIO_ADAPTER"></span>


本部分包括有关安装端口类音频适配器的核心系统组件的以下主题：

[在 Windows 中安装](installing-in-windows.md)

[ **INF DDInstall 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547344)为每个硬件制造中指定 ID**模型**部分应指定包含**KS。注册**Ks.inf 中的部分和**WDMAUDIO。注册**Wdmaudio.inf 中的部分。 Ks.inf 文件将安装核心内核流式处理组件。 Wdmaudio.inf 文件将安装核心 WDM 音频组件。 供应商不应修改或替换这些系统 INF 文件。

 

 




