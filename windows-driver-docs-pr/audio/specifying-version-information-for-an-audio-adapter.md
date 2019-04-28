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
ms.openlocfilehash: f79b19799bbb1aa8c4def21888b97c31d6ad769b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328615"
---
# <a name="specifying-version-information-for-an-audio-adapter"></a>指定音频适配器的版本信息


## <span id="specifying_version_information_for_an_audio_adapter"></span><span id="SPECIFYING_VERSION_INFORMATION_FOR_AN_AUDIO_ADAPTER"></span>


供应商应指定中的以下条目**版本**端口类音频适配器对 INF 文件的部分：

```inf
  Signature="$CHICAGO$"
  Class=MEDIA
  ClassGUID={4d36e96c-e325-11ce-bfc1-08002be10318}
```

有关其他版本要求和选项的所有设备类的说明，请参阅[ **INF 版本部分**](https://msdn.microsoft.com/library/windows/hardware/ff547502)。

 

 




