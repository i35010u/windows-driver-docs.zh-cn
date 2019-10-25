---
title: KSPROPSETID\_SoundDetector2
description: KSPROPSETID_SoundDetector2 属性集包含的属性用于为也支持检测程序的音频捕获设备注册筛选器。
ms.assetid: FC4A354B-D42C-4199-B613-1E1B75A600C7
ms.date: 09/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: 025fa4aeb052308a69752770c55d05fce1df1fa4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830472"
---
# <a name="kspropsetid_sounddetector2"></a>KSPROPSETID\_SoundDetector2

`KSPROPSETID_SoundDetector2` 属性集包含的属性用于为也支持检测程序的音频捕获设备注册筛选器。 该筛选器有一个包含 pin 类别 KSNODETYPE 的 KS pin 工厂， [\_音频\_KEYWORDDETECTOR](ksnodetype-audio-keyworddetector.md)。 给定 KS 筛选器实例中不能有多个具有此 KS pin 类别的 pin 工厂。

Windows 10 版本1903及更高版本支持 `KSPROPSETID_SoundDetector2`。 KSPROPSETID_SoundDetector2 属性集用于支持多个语音代理。 有关详细信息，请参阅[多个语音助手](voice-activation-mva.md)。  在仅支持 Cortana 的系统上使用[KSPROPSETID\_SoundDetector](kspropsetid-sounddetector.md)属性集。  

`KSPROPSETID_SoundDetector2` 使用[KSSOUNDDETECTORPROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kssounddetectorproperty)结构，而不是 KSPROPERTY：

``` syntax
typedef struct {
    KSPROPERTY  Property;
    GUID        EventId;
} KSSOUNDDETECTORPROPERTY, *PKSSOUNDDETECTORPROPERTY;
```

使用[KSSOUNDDETECTORPROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kssounddetectorproperty)数据结构调用所有 KSPROPSETID_SoundDetector2 属性。 此数据结构包含 KSPROPERTY 以及要识别、重置、检测到的关键字的事件 id。

标头文件定义**KSPROPSETID\_SoundDetector2**属性集，如下所示：

``` syntax
#define STATIC_KSPROPSETID_SoundDetector2\
    0xfe07e322, 0x450c, 0x4bd5, 0x84, 0xca, 0xa9, 0x48, 0x50, 0xe, 0xa6, 0xaa
DEFINE_GUIDSTRUCT("FE07E322-450C-4BD5-84CA-A948500EA6AA", KSPROPSETID_SoundDetector2);
```

`KSPROPSETID_SoundDetector2` 属性集包含以下属性：

- [KSPROPERTY\_SOUNDDETECTOR\_SUPPORTEDPATTERNS](ksproperty-sounddetector-supportedpatterns.md) -此属性由操作系统设置，用于配置要检测的关键字。

- [KSPROPERTY\_SOUNDDETECTOR\_模式](ksproperty-sounddetector-patterns.md)-驱动程序的 KS 筛选器支持此读/写属性。 OS 设置此属性以配置要检测的关键字。

- [KSPROPERTY\_SOUNDDETECTOR\_](ksproperty-sounddetector-armed.md)预知道，此读取/写入属性是一个简单的布尔状态，指示检测程序是否已确定。 操作系统将此设置为参与关键字检测器。 操作系统可以清除此来脱开。 如果设置了关键字模式，并且在检测到了关键字之后，驱动程序会自动清除此设置。 （操作系统必须进行重置。）

- [KSPROPERTY\_SOUNDDETECTOR\_reset](ksproperty-sounddetector-reset.md) -重置检测程序到无模式集的 unarmed 状态。

- [KSPROPERTY\_SOUNDDETECTOR\_STREAMINGSUPPORT](ksproperty-sounddetector-streamingsupport.md) -仅供语音开始检测程序使用。 此请求失败指示属性不受支持或成功，并为所有其他驱动程序返回 true。

在关键字检测时，会发送包含 KSNOTIFICATIONID_SoundDetector 的 PNP 通知。 注意：这不是 KSEvent，而是使用负载通过[IoReportTargetDeviceChangeAsynchronous](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreporttargetdevicechangeasynchronous)发送的 PNP 事件。
