---
title: 指定音频适配器的版本信息
description: 指定音频适配器的版本信息
ms.assetid: 2d1fb5e7-84fe-451f-b53f-bf6017ae94ad
keywords:
- 音频适配器 WDK，版本信息
- 适配器驱动程序 WDK 音频，版本信息
- 端口类音频适配器 WDK，版本信息
- 版本 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1811d2f12e0fbe758179b4fa9c77713bb752b849
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210385"
---
# <a name="specifying-version-information-for-an-audio-adapter"></a>指定音频适配器的版本信息


## <span id="specifying_version_information_for_an_audio_adapter"></span><span id="SPECIFYING_VERSION_INFORMATION_FOR_AN_AUDIO_ADAPTER"></span>


供应商应在端口类音频适配器的 INF 文件的 **版本** 部分中指定以下各项：

```inf
  Signature="$CHICAGO$"
  Class=MEDIA
  ClassGUID={4d36e96c-e325-11ce-bfc1-08002be10318}
```

有关所有设备类的其他版本要求和选项的说明，请参阅 [**INF 版本部分**](../install/inf-version-section.md)。

 

