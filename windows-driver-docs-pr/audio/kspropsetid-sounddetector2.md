---
title: KSPROPSETID \_ SoundDetector2
description: KSPROPSETID_SoundDetector2 属性集包含用于为同时支持检测程序的音频捕获设备注册筛选器的属性。
ms.date: 09/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: eec6ec010458b7fa707d8e461ef56c43c67b5c83
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801077"
---
# <a name="kspropsetid_sounddetector2"></a>KSPROPSETID \_ SoundDetector2

`KSPROPSETID_SoundDetector2`属性集包含的属性用于为也支持检测程序的音频捕获设备注册筛选器。 该筛选器具有具有 pin 类别 [KSNODETYPE \_ AUDIO \_ KEYWORDDETECTOR](ksnodetype-audio-keyworddetector.md)的 KS pin 工厂。 给定 KS 筛选器实例中不能有多个具有此 KS pin 类别的 pin 工厂。

`KSPROPSETID_SoundDetector2` 在 Windows 10 版本1903及更高版本中受支持。 KSPROPSETID_SoundDetector2 属性集用于支持多个语音代理。 有关详细信息，请参阅 [多个语音助手](voice-activation-mva.md)。  [KSPROPSETID \_SoundDetector](kspropsetid-sounddetector.md) 属性集用于仅支持 Cortana 的系统。  

`KSPROPSETID_SoundDetector2` 使用 [KSSOUNDDETECTORPROPERTY](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kssounddetectorproperty) 结构，而不是 KSPROPERTY：

``` syntax
typedef struct {
    KSPROPERTY  Property;
    GUID        EventId;
} KSSOUNDDETECTORPROPERTY, *PKSSOUNDDETECTORPROPERTY;
```

所有 KSPROPSETID_SoundDetector2 属性都是使用 [KSSOUNDDETECTORPROPERTY](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kssounddetectorproperty)  数据结构调用的。 此数据结构包含 KSPROPERTY 以及要识别、重置、检测到的关键字的事件 id。

标头文件定义 **KSPROPSETID \_ SoundDetector2** 属性集，如下所示：

``` syntax
#define STATIC_KSPROPSETID_SoundDetector2\
    0xfe07e322, 0x450c, 0x4bd5, 0x84, 0xca, 0xa9, 0x48, 0x50, 0xe, 0xa6, 0xaa
DEFINE_GUIDSTRUCT("FE07E322-450C-4BD5-84CA-A948500EA6AA", KSPROPSETID_SoundDetector2);
```

`KSPROPSETID_SoundDetector2`属性集包含以下属性：

- [KSPROPERTY \_SOUNDDETECTOR \_ SUPPORTEDPATTERNS](ksproperty-sounddetector-supportedpatterns.md) -此属性由操作系统设置，用于配置要检测的关键字。

- [KSPROPERTY \_SOUNDDETECTOR \_ 模式](ksproperty-sounddetector-patterns.md) -驱动程序的 KS 筛选器支持此读/写属性。 OS 设置此属性以配置要检测的关键字。

- [KSPROPERTY \_SOUNDDETECTOR \_ ](ksproperty-sounddetector-armed.md) -此读取/写入属性是一个简单的布尔状态，它指示是否已配备了检测程序。 操作系统将此设置为参与关键字检测器。 操作系统可以清除此来脱开。 如果设置了关键字模式，并且在检测到了关键字之后，驱动程序会自动清除此设置。  (操作系统必须进行重置。 ) 

- [KSPROPERTY \_SOUNDDETECTOR \_ 重置](ksproperty-sounddetector-reset.md) -将检测程序重置为不带模式集的 unarmed 状态。

- [KSPROPERTY \_SOUNDDETECTOR \_ STREAMINGSUPPORT](ksproperty-sounddetector-streamingsupport.md) -仅供语音开始检测程序使用。 此请求失败指示属性不受支持或成功，并为所有其他驱动程序返回 true。

在关键字检测时，将发送包含 KSNOTIFICATIONID_SoundDetector 的 PNP 通知。 注意：这不是 KSEvent，而是使用负载通过 [IoReportTargetDeviceChangeAsynchronous](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreporttargetdevicechangeasynchronous)发送的 PNP 事件。
