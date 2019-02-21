---
title: 蓝牙 HFP DDI 引用
description: Windows 8 引入了 GUID\_DEVINTERFACE\_蓝牙\_HFP\_SCO\_HCIBYPASS 类，无需手动为实现 I/O 控制代码 (Ioctl) 和结构的接口配置文件 (HFP) 绕过音频驱动程序。
ms.assetid: 980B7283-56C5-44FA-8992-6DA5BE263FCD
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5bee5b4f82889094e99f97b2105345088562ab0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543359"
---
# <a name="bluetooth-hfp-ddi-reference"></a>蓝牙 HFP DDI 引用


Windows 8 引入了 GUID\_DEVINTERFACE\_蓝牙\_HFP\_SCO\_HCIBYPASS 类，无需手动为实现 I/O 控制代码 (Ioctl) 和结构的接口配置文件 (HFP) 绕过音频驱动程序。

为每个配对的蓝牙设备 HFP 上 HFP 驱动程序注册此类中的接口。 该接口是注册和配对设备和 HFP 驱动程序运行后启用。 当驱动程序停止时，接口是禁用并注销。

当开发用于绕过音频连接蓝牙控制器上的驱动程序时，您的驱动程序可以使用这些接口来完全实现蓝牙音频支持。 HFP 设备允许只有单个文件对象上 GUID\_DEVINTERFACE\_蓝牙\_HFP\_SCO\_HCIBYPASS 设备接口。

以下主题介绍的结构和为此类定义的 Ioctl。

[蓝牙 HFP DDI 结构](bluetooth-hfp-ddi-structures.md)

[蓝牙 HFP DDI Ioctl](bluetooth-hfp-ddi-ioctls.md)

 

 





