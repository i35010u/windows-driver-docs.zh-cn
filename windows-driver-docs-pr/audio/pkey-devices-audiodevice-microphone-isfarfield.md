---
title: PKEY \_ 设备 \_ AudioDevice \_ 麦克风 \_ IsFarField
description: 在 Windows 10 版本19H1 和更高版本中， **PKEY \_ 设备 \_ AudioDevice \_ 麦克风 \_ IsFarField** 属性键标识指示麦克风是否将捕获 far 现场音频。
ms.date: 02/13/2019
ms.localizationpriority: medium
ms.openlocfilehash: cb3b9aaf49d7fe16234098aa1a07f29316131411
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210489"
---
# <a name="pkey_devices_audiodevice_microphone_isfarfield"></a>PKEY \_ 设备 \_ AudioDevice \_ 麦克风 \_ IsFarField

在 Windows 10 19H1 和更高版本中， **PKEY \_ 设备 \_ AudioDevice \_ 麦克风 \_ IsFarField** 属性键指示麦克风是否将捕获 far 现场音频。

从 Windows 10 19H1 开始，使用 PKEY \_ 设备 \_ AudioDevice \_ 麦克风 \_ IsFarField 属性是支持 far 现场音频的系统的一项要求，通常用于语音助手。

如果值为1，则表示麦克风将捕获 far 现场音频，这会使麦克风成为语音助手的首选端点。

如果值为0或没有属性键，则指示麦克风不支持 far 现场或支持未知，因此，不会将端点的优先顺序用于语音助手。

此属性应通过 INF 设置，最好是由 OEM 提供的扩展 INF，而不是音频设备的基本 INF。 有关扩展 INF 文件的详细信息，请参阅 [创建组件化音频驱动程序安装](./audio-universal-drivers.md#creating-a-componentized-audio-driver-installation) 和 [使用扩展 inf 文件](../install/using-an-extension-inf-file.md)。

## <a name="inf-file-sample"></a>INF 文件示例

Sysvad 示例 ComponentizedAudioSampleExtension 文件包含此属性。 此示例显示设置为0x1 的值，指示麦克风捕获远距离现场音频。

```inf
;HKR,EP\1,%PKEY_Devices_AudioDevice_Microphone_IsFarField%,0x00010001,0x1
```

## <a name="requirements"></a>要求

|要求|值 |
|--- |--- |
|最低受支持的客户端|Windows 10 版本19H1|
|标头|Ksmedia.h|

## <a name="related-topics"></a>相关主题

[媒体类 INF 扩展](media-class-inf-extensions.md)