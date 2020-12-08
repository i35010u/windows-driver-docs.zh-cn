---
title: 音频驱动程序枚举
description: 本部分介绍各种音频属性和结构所使用的枚举。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c28ea1eab368bd00b1229437f3ff9e0130a01844
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785005"
---
# <a name="audio-drivers-enumerations"></a>音频驱动程序枚举


本部分介绍各种音频属性和结构所使用的枚举。

## <a name="span-idwindows_10_and_later_operating_systemsspanspan-idwindows_10_and_later_operating_systemsspanspan-idwindows_10_and_later_operating_systemsspanwindows-10-and-later-operating-systems"></a><span id="Windows_10_and_later_operating_systems"></span><span id="windows_10_and_later_operating_systems"></span><span id="WINDOWS_10_AND_LATER_OPERATING_SYSTEMS"></span>Windows 10 及更高版本的操作系统


以下枚举用于 Windows 10 及更高版本的操作系统：

[**电话服务 \_CALLCONTROLOP**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-telephony_callcontrolop)。 由音频驱动程序结构用来指定要在电话呼叫上执行的操作。

[**电话服务 \_CALLSTATE**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-telephony_callstate)。 由音频驱动程序结构用来指定电话呼叫的状态。

[**电话服务 \_CALLTYPE**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-telephony_calltype)。 由音频驱动程序结构用于指定电话号码类型。

[**电话服务 \_PROVIDERCHANGEOP**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-telephony_providerchangeop)。 由音频驱动程序结构用来指定提供程序所请求的更改操作的类型。

## <a name="span-idwindows_8_and_later_operating_systemsspanspan-idwindows_8_and_later_operating_systemsspanspan-idwindows_8_and_later_operating_systemsspanwindows-8-and-later-operating-systems"></a><span id="Windows_8_and_later_operating_systems"></span><span id="windows_8_and_later_operating_systems"></span><span id="WINDOWS_8_AND_LATER_OPERATING_SYSTEMS"></span>Windows 8 及更高版本的操作系统


以下枚举用于 Windows 8 及更高版本的操作系统：

[**音频 \_曲线 \_ 类型**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-audio_curve_type)。 由音频驱动程序结构用来指示应应用于卷级别控制的音频数据流的曲线算法的类型。

[**EPcMiniportEngineEvent**](/windows-hardware/drivers/ddi/portcls/ne-portcls-epcminiportengineevent)。 由音频引擎用来提供与 glitching 错误相关的信息。

[**PC \_退出 \_ 延迟**](/windows-hardware/drivers/ddi/portcls/ne-portcls-_pc_exit_latency)。 由音频端口类驱动程序使用 (PortCls) ，以指示退出休眠状态和进入完全功能状态的最大延迟时间。

[**eEngineFormatType**](/windows-hardware/drivers/ddi/portcls/ne-portcls-eengineformattype)。 由微型端口驱动程序用来指示音频引擎支持的数据格式类型。

[**eChannelTargetType**](/windows-hardware/drivers/ddi/portcls/ne-portcls-echanneltargettype)。 由微型端口驱动程序用来指示 (目标) 在音频数据流路径中的节点类型。

## <a name="span-idwindows_7_and_earlier_operating_systemsspanspan-idwindows_7_and_earlier_operating_systemsspanspan-idwindows_7_and_earlier_operating_systemsspanwindows-7-and-earlier-operating-systems"></a><span id="Windows_7_and_earlier_operating_systems"></span><span id="windows_7_and_earlier_operating_systems"></span><span id="WINDOWS_7_AND_EARLIER_OPERATING_SYSTEMS"></span>Windows 7 和更早版本的操作系统


以下枚举是在 Windows 7 及更早版本的操作系统中引入的：

[**KSPROPERTY \_AUDIOENGINE**](ksproperty-audioengine.md)。 由微型端口驱动程序用来指定音频引擎的属性和设置参数。

[**KSPROPERTY \_插孔**](ksproperty-jack.md)。 由微型端口驱动程序用来指定音频终结点插孔的属性。

 

