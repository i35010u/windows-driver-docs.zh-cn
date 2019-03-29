---
title: Windows 类 vs。接口类
description: Windows 类 vs。
ms.assetid: 3df99388-6fcf-44bb-a6c9-99281a8879d7
keywords:
- 设备接口的类 WDK 设备安装
- 设备安装程序类 WDK 设备安装
- 接口类 WDK 设备安装
- 安装程序类 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32abd3b58e55b8316e650fdb11bd175264025148
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569055"
---
# <a name="windows-classes-vs-interface-classes"></a>Windows 类 vs。接口类





务必要区分两种类型的设备类： [*设备接口类*](device-interface-classes.md)并[*设备安装程序类*](device-setup-classes.md)。 这两个可以容易混淆因为在用户模式代码中，同一套[设备安装函数](https://msdn.microsoft.com/library/windows/hardware/ff541299)和一组相同的数据结构 ([设备信息设置](device-information-sets.md)) 与这两个类一起使用。 此外，设备通常属于安装程序类和接口的多个类都在同一时间。 不过，两种类型的类满足不同目的，请使用的不同方面在注册表中，并依赖于一组不同的定义类 Guid 的标头文件。

[设备安装程序类](device-setup-classes.md)提供用于对设备的安装和配置相同的方式进行分组的机制。 安装程序类标识类安装程序和安装属于此类设备所涉及的类共同安装程序。 例如，所有的 CD-ROM 驱动器属于 CDROM 安装程序类，将使用相同的共同安装程序时安装。

[设备接口类](device-interface-classes.md)提供用于对根据共享的特征的设备进行分组的机制。 而不是跟踪单个设备的系统中存在，驱动程序和用户应用程序可以注册的到达或属于某个特定的接口类的任何设备中删除的通知。

系统文件中定义 Windows 类*Devguid.h*。 此文件定义安装程序类的一系列的 Guid。 但是，设备安装程序类表示在*Devguid.h*不能与设备相混淆*接口*类。 *Devguid.h*文件仅包含用于安装程序类 Guid。

单个文件中未提供的接口的类定义。 设备接口类始终以独占方式属于设备的特定类的头文件中定义。 例如， *Ntddmou.h*包含 GUID_CLASS_MOUSE，表示鼠标接口类; 的 GUID 的定义*Ntddpar.h*定义并行设备; 的接口类 GUID*Ntddpcm.h*定义 PCMCIA 设备; 的标准接口，类 GUID*Ntddstor.h*定义用于存储设备等的接口类 GUID。

应使用特定于设备接口类的标头文件中的 Guid 来注册通知到达设备接口的实例。 如果驱动程序注册通知使用安装程序类 GUID 而不接口类 GUID，然后它将不会到达时通知接口。

定义新的安装程序类或接口类时*不使用单一 GUID 来标识安装程序类和接口类。*

有关 Guid 的详细信息，请参阅[驱动程序中使用 Guid](https://msdn.microsoft.com/library/windows/hardware/ff565392)。

 

 





