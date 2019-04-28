---
title: 音频驱动程序枚举
description: 本部分介绍各种音频属性和结构所使用的枚举。
ms.assetid: 9C7530BE-C63F-438C-A853-9A7E47C240E9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d1ec48b69ed7c04c4b2dcdda36252456c67e783
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331539"
---
# <a name="audio-drivers-enumerations"></a>音频驱动程序枚举


本部分介绍各种音频属性和结构所使用的枚举。

## <a name="span-idwindows10andlateroperatingsystemsspanspan-idwindows10andlateroperatingsystemsspanspan-idwindows10andlateroperatingsystemsspanwindows10-and-later-operating-systems"></a><span id="Windows_10_and_later_operating_systems"></span><span id="windows_10_and_later_operating_systems"></span><span id="WINDOWS_10_AND_LATER_OPERATING_SYSTEMS"></span>Windows 10 和更高版本操作系统


Windows 10 和更高版本操作系统中使用了以下枚举：

[**电话\_CALLCONTROLOP**](https://msdn.microsoft.com/library/windows/hardware/mt169895)。 使用音频驱动程序结构来指定要在电话上执行的操作。

[**电话\_CALLSTATE**](https://msdn.microsoft.com/library/windows/hardware/mt169896)。 使用音频驱动程序结构来指定电话呼叫的状态。

[**电话\_CALLTYPE**](https://msdn.microsoft.com/library/windows/hardware/mt169897)。 音频驱动程序结构使用它来指定电话呼叫的类型。

[**电话\_PROVIDERCHANGEOP**](https://msdn.microsoft.com/library/windows/hardware/mt169898)。 使用音频驱动程序结构来指定提供程序请求的更改操作的类型。

## <a name="span-idwindows8andlateroperatingsystemsspanspan-idwindows8andlateroperatingsystemsspanspan-idwindows8andlateroperatingsystemsspanwindows8-and-later-operating-systems"></a><span id="Windows_8_and_later_operating_systems"></span><span id="windows_8_and_later_operating_systems"></span><span id="WINDOWS_8_AND_LATER_OPERATING_SYSTEMS"></span>Windows 8 和更高版本操作系统


Windows 8 和更高版本操作系统中使用以下枚举：

[**音频\_曲线\_类型**](https://msdn.microsoft.com/library/windows/hardware/hh831852)。 使用音频驱动程序结构来指示应将应用到卷级别控制的音频数据流的曲线算法的类型。

[**EPcMiniportEngineEvent**](https://msdn.microsoft.com/library/windows/hardware/dn302036)。 由音频引擎来提供与干扰错误相关的信息。

[**PC\_退出\_延迟**](https://msdn.microsoft.com/library/windows/hardware/dn265130)。 音频端口类驱动程序 (PortCls) 用于指示有关退出正在睡眠状态的最大延迟时间状态和输入的完全正常运行状态。

[**eEngineFormatType**](https://msdn.microsoft.com/library/windows/hardware/dn302035)。 使用的微型端口驱动程序，以指示数据设置格式的音频引擎支持的类型。

[**eChannelTargetType**](https://msdn.microsoft.com/library/windows/hardware/dn302034)。 由微型端口驱动程序来指示类型的音频数据流路径中的节点 （目标）。

## <a name="span-idwindows7andearlieroperatingsystemsspanspan-idwindows7andearlieroperatingsystemsspanspan-idwindows7andearlieroperatingsystemsspanwindows7-and-earlier-operating-systems"></a><span id="Windows_7_and_earlier_operating_systems"></span><span id="windows_7_and_earlier_operating_systems"></span><span id="WINDOWS_7_AND_EARLIER_OPERATING_SYSTEMS"></span>Windows 7 和更早的操作系统


Windows 7 和更早的操作系统中引入了以下枚举：

[**KSPROPERTY\_AUDIOENGINE**](ksproperty-audioengine.md)。 由微型端口驱动程序用于指定属性和安装参数，以音频引擎。

[**KSPROPERTY\_JACK**](ksproperty-jack.md)。 由微型端口驱动程序用于指定终结点音频插孔的属性。

 

 





