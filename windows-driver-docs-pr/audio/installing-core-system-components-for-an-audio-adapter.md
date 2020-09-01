---
title: 为音频适配器安装核心系统组件
description: 为音频适配器安装核心系统组件
ms.assetid: fc14867e-cae8-4381-bcd3-ec2230050cf6
keywords:
- 音频适配器 WDK，系统组件
- 适配器驱动程序 WDK 音频，系统组件
- 端口类音频适配器 WDK，系统组件
ms.date: 10/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38ca95cd2e9281ed3395ab094549e5de8df13026
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209113"
---
# <a name="installing-core-system-components-for-an-audio-adapter"></a>为音频适配器安装核心系统组件


## <span id="installing_core_system_components_for_an_audio_adapter"></span><span id="INSTALLING_CORE_SYSTEM_COMPONENTS_FOR_AN_AUDIO_ADAPTER"></span>


本部分包括有关安装端口类音频适配器的核心系统组件的以下主题：

[在 Windows 中安装](installing-in-windows.md)

在制造商的 "**模型**" 部分中指定的每个硬件 ID 的 " [**INF DDInstall" 部分**](../install/inf-ddinstall-section.md)应指定是否包含**KS。** WDMAUDIO 中的注册部分。 **WDMAUDIO.Registration**Wdmaudio 中的注册部分。 Ks 文件安装核心内核流式处理组件。 Wdmaudio 文件安装核心 WDM 音频组件。 供应商不应修改或替换这些系统 INF 文件。

 

