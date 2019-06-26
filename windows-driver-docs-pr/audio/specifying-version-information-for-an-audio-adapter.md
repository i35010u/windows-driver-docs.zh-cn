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
ms.openlocfilehash: b5cd4405c69a99679194c144b2a5684c29877f24
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354285"
---
# <a name="specifying-version-information-for-an-audio-adapter"></a>指定音频适配器的版本信息


## <span id="specifying_version_information_for_an_audio_adapter"></span><span id="SPECIFYING_VERSION_INFORMATION_FOR_AN_AUDIO_ADAPTER"></span>


供应商应指定中的以下条目**版本**端口类音频适配器对 INF 文件的部分：

```inf
  Signature="$CHICAGO$"
  Class=MEDIA
  ClassGUID={4d36e96c-e325-11ce-bfc1-08002be10318}
```

有关其他版本要求和选项的所有设备类的说明，请参阅[ **INF 版本部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)。

 

 




