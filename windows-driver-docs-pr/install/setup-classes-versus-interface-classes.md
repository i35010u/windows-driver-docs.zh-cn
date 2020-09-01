---
title: Windows 类与接口类
description: Windows 类与
ms.assetid: 3df99388-6fcf-44bb-a6c9-99281a8879d7
keywords:
- 设备接口类 WDK 设备安装
- 设备安装程序类 WDK 设备安装
- 接口类 WDK 设备安装
- 安装类 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f22a26aabf0e150d2de5b4fd36ac0d86140e7b8c
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097175"
---
# <a name="windows-classes-vs-interface-classes"></a>Windows 类与接口类





区分设备[*类和设备*](./overview-of-device-interface-classes.md)[*安装程序类*](./overview-of-device-setup-classes.md)，这一点很重要。 这两个方法很容易混淆，因为在用户模式代码中，同一组 [设备安装功能](/previous-versions/ff541299(v=vs.85)) 和相同的数据结构集 ([设备信息集](device-information-sets.md)) 与这两个类一起使用。 此外，设备通常同时属于安装类和多个接口类。 尽管如此，这两种类型的类提供不同的用途，使用注册表中的不同区域，并依赖一组不同的标头文件来定义类 Guid。

[设备安装程序类](./overview-of-device-setup-classes.md) 提供一种机制，用于将以相同方式安装和配置的设备进行分组。 安装类标识安装属于类的设备所涉及的类安装程序和类共同安装程序。 例如，所有 cd-rom 驱动器都属于 CDROM 安装程序类，安装时将使用相同的共同安装程序。

[设备接口类](./overview-of-device-interface-classes.md) 提供一种机制，用于根据共享特征对设备进行分组。 无需跟踪单个设备的系统中的状态，驱动程序和用户应用程序就可以注册，以获得有关属于特定接口类的任何设备的到达或删除通知。

Windows 类在系统文件 *Devguid*中定义。 此文件为安装程序类定义了一系列 Guid。 但是， *Devguid* 中表示的设备安装程序类不得与设备 *接口* 类混淆。 *Devguid*文件仅包含安装程序类的 guid。

不在单个文件中提供接口类的定义。 设备接口类始终在仅属于特定设备类的标头文件中定义。 例如， *Ntddmou* 包含 GUID_CLASS_MOUSE 的定义，GUID 表示鼠标接口类; *Ntddpar* 定义用于并行设备的接口类 GUID; *Ntddpcm* 定义 PCMCIA 设备的标准接口类 GUID; *Ntddstor* 定义存储设备的接口类 GUID，依此类推。

应使用特定于设备接口类的标头文件中的 Guid 来注册设备接口实例的到达通知。 如果驱动程序使用安装程序类 GUID 而不是接口类 GUID 来注册通知，则接口到达时将不会通知该驱动程序。

定义新的安装类或接口类时，请不要 *使用单个 GUID 来标识安装类和接口类。*

有关 Guid 的详细信息，请参阅 [在驱动程序中使用 guid](../kernel/using-guids-in-drivers.md)。

 

