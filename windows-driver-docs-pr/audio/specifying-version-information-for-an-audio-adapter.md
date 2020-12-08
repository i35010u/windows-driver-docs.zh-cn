---
title: 指定音频适配器的版本信息
description: 指定音频适配器的版本信息
keywords:
- 音频适配器 WDK，版本信息
- 适配器驱动程序 WDK 音频，版本信息
- 端口类音频适配器 WDK，版本信息
- 版本 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa87339601e59c3f117d7bfeb34d1f8751ddc3a5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800625"
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

 

