---
title: PKEY\_Devices\_AudioDevice\_Microphone\_IsFarField
description: 在 Windows 10 版本 19 H 1 及更高版本，**主键\_设备\_AudioDevice\_麦克风\_IsFarField**属性键标识指示麦克风将捕获远端字段音频。
ms.date: 02/13/2019
ms.localizationpriority: medium
ms.openlocfilehash: 89a38c5cd59318c13d9c1e7ce248bad62eb1138f
ms.sourcegitcommit: 5f4404a7010a6b26530f60144c5ea7cab846feec
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2019
ms.locfileid: "56582907"
---
# <a name="pkeydevicesaudiodevicemicrophoneisfarfield"></a>PKEY\_Devices\_AudioDevice\_Microphone\_IsFarField

Windows 10 中 1 及更高版本，19 H**主键\_设备\_AudioDevice\_麦克风\_IsFarField**属性键指示麦克风是否将捕获得字段音频。 

Windows 10 中启动 19 H 1，使用主键\_设备\_AudioDevice\_麦克风\_IsFarField 属性是必需的目前支持的系统字段音频，通常以供语音助手。 

如果值为 1 指示麦克风将得捕获字段音频，这将麦克风的首选的端点的语音助手。 

值为 0 或任何属性键指示麦克风不支持延伸的范围的字段或支持为未知的因此通过语音助手不使用优先终结点。

该属性应设置通过 INF，和最好是 OEM 提供的而不是基 INF 的音频设备扩展 INF。 有关扩展 INF 文件的详细信息，请参阅[创建的组件化的音频驱动程序安装](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-universal-drivers#-creating-a-componentized-audio-driver-installation)并[使用扩展 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/using-an-extension-inf-file)。




## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF 文件示例

Sysvad 示例 ComponentizedAudioSampleExtension.inf 文件包含此属性。 此示例演示将值设置为 0x1，该值指示麦克风 does 捕获得字段音频。

```inf
;HKR,EP\1,%PKEY_Devices_AudioDevice_Microphone_IsFarField%,0x00010001,0x1
```

<a name="requirements"></a>要求
------------

|||
|--- |--- |
|最低受支持的客户端|Windows 10 版本 19 H 1|
|Header|Ksmedia.h|

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[媒体类 INF 扩展](media-class-inf-extensions.md)

 

 






