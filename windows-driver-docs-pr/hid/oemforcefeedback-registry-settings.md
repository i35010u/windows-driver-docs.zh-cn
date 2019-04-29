---
title: OEMForceFeedback 注册表设置
description: OEMForceFeedback 注册表设置
ms.assetid: c29fe1e8-1cd9-4b32-96d7-1afae5a49d42
keywords:
- 强制反馈驱动程序 WDK HID，OEMForceFeedback settiings
- WDK HID OEMForceFeedback 密钥
- 注册表 WDK 强制反馈
- 效果子项 WDK 强制反馈
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c45de6bfdd67ee517dfeac41acb3292dcd57ba9d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373004"
---
# <a name="oemforcefeedback-registry-settings"></a>OEMForceFeedback 注册表设置





新游戏杆的注册表项下的注册表路径与项下每个游戏杆设备类型安装特定于 OEM 的密钥可找到**HKEY\_本地\_机\\系统\\CurrentControlSet\\控制\\MediaProperties\\PrivateProperties\\游戏杆\\OEM**。 在此特定于 OEM 的密钥存储的数据被初始化时该设备是首次安装，则用于参考目的。 除了为现有的游戏杆设备定义的值、 两个新的可选泛型值和强制的一组已定义反馈特定值。

两个泛型值是一个包含版本信息的二进制值和一个**制造商**的字符串值 (REGSTR\_VAL\_regstr.h 制造商提供) 包含制造商的名称的字符串。 后者是现有补充**OEMName**值，该值包含设备的名称。

一个新**OEMForceFeedback**定义键以包含强制反馈特定键和值。 此项下是**效果**子项包含两个值的每个效果。

下**效果**子项是一个用于每个效果的子项的列表。 每个子项的名称是全局唯一标识符 (GUID) 在窗体"{12345678-1234-1234-1234-123456789012}"。 下名为"{...}"的密钥 是两个值。 默认值为字符串的效果的友好名称。 **特性**值是[ **DIEFFECTATTRIBUTES** ](https://msdn.microsoft.com/library/windows/hardware/ff538456)结构。

```cpp
"{guid1}"
    Default value = friendly name for effect {guid1} (string)
    "Attributes" = DIEFFECTATTRIBUTES structure (binary)
"{guid2}"
    Default value = friendly name for effect {guid2} (string)
    "Attributes" = DIEFFECTATTRIBUTES structure (binary)
```

**OEMForceFeedback**键还包含一个值，包含的设备属性和两个可选值之一。 可选值，使用**CLSID**如果您使用的 3 环驱动程序 (DLL) 和**VJoyD**如果使用的 ring 0 驱动程序 (VxD)。

```cpp
"Attributes" = DIFFDEVICEATTRIBUTES structure (binary)
"CLSID" = {GUID} for force feedback effect driver (string)(optional)
"VJoyD" = zero-length binary (optional)
```

可选值的名称指示使用哪种形式的接口。 如果**CLSID**值不存在，应为包含窗体中的 GUID 的字符串值"{12345678-1234-1234-1234-123456789012}"提供了驱动程序接口的 COM 对象。 如果**VJoyD**值存在时，它应该是长度为零的二进制值，该值指示 VJoyD 微型驱动程序与设备关联要使用应为驱动程序接口提供额外的回调。 添加值来指示，人机接口设备 (HID) 提供了驱动程序接口时实现。

如果设备支持的硬件效果不属于任何预定义的类别 (DIEFT\_CONSTANTFORCE、 DIEFT\_RAMPFORCE、 DIEFT\_定期、 DIEFT\_条件或 DIEFT\_CUSTOMFORCE)，则[ **DIEFFECTATTRIBUTES** ](https://msdn.microsoft.com/library/windows/hardware/ff538456)结构的影响应指定 DIEFT\_作为效果类型的硬件。

设备可以支持处于某个预定义的类别 （在上一段中列出） 中的硬件效果，但还会收到不是标准的特定于类型的数据结构 （DICONSTANTFORCE、 DIRAMPFORCE 的一部分的其他参数DIPERIODIC、 DICONDITION 或 DICUSTOMFORCE）。 有关这些结构的信息，请参阅 DirectInput 部分的 DirectX 软件开发工具包 (SDK)。 在这些情况下，效果应列出两次，如下所示：

-   列出预定义的类别下的效果。 如果应用程序中预定义的类别创建效果，该驱动程序应提供适当的默认值为指定的参数不是标准的特定于类型的数据结构的一部分。

-   列表下 DIEFT 效果\_硬件类别。 创建特殊的特定于类型的结构 （如 DIPERIODICFORCEWITHDECAY)，其中包含额外的参数。

以这种方式，为你的硬件设计的应用程序可以使用第二个效果描述符来访问的所有功能的效果，而泛型硬件设计的应用程序可以使用第一个效果描述符都访问基本功能的效果。

 

 




