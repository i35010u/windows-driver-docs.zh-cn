---
title: 蓝牙 HFP DDI 参考
description: Windows 8 引入了 GUID \_ DEVINTERFACE \_ 蓝牙 \_ HFP \_ SCO \_ HCIBYPASS 类，其中接口实现 i/o 控制代码 (IOCTLs) 和用于免提配置文件的结构 (HFP) 绕过音频驱动程序。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: eebcd95a84a103b729e6798ea017f9da9ff41ba7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784925"
---
# <a name="bluetooth-hfp-ddi-reference"></a>蓝牙 HFP DDI 参考


Windows 8 引入了 GUID \_ DEVINTERFACE \_ 蓝牙 \_ HFP \_ SCO \_ HCIBYPASS 类，其中接口实现 i/o 控制代码 (IOCTLs) 和用于免提配置文件的结构 (HFP) 绕过音频驱动程序。

对于配对蓝牙设备上的每个 HFP，HFP 驱动程序将在此类中注册一个接口。 设备配对并且 HFP 驱动程序正在运行后，将注册并启用接口。 当驱动程序停止时，接口被禁用并取消注册。

开发用于在蓝牙控制器上绕过音频连接的驱动程序时，驱动程序可以使用这些接口来完全实现蓝牙音频支持。 HFP 设备仅允许 GUID \_ DEVINTERFACE \_ 蓝牙 \_ HFP \_ SCO \_ HCIBYPASS 设备接口上的单个文件对象。

以下主题介绍为此类定义的结构和 IOCTLs。

[蓝牙 HFP DDI 结构](bluetooth-hfp-ddi-structures.md)

[蓝牙 HFP DDI IOCTL](bluetooth-hfp-ddi-ioctls.md)

 

 





