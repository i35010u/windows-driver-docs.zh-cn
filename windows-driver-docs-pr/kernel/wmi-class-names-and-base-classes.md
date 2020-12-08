---
title: WMI 类名和基类
description: WMI 类名和基类
keywords:
- 基类 WDK WMI
- 命名 WDK WMI
- 类 WDK WMI
- WMI WDK 内核，类
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bef12b7a39515ab2ef616510578aa5e4ec44ef84
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782681"
---
# <a name="wmi-class-names-and-base-classes"></a>WMI 类名和基类





WMI 类名称不区分大小写，必须以字母开头，并且不能以下划线开头或结尾。 剩余的所有字符都必须是字母、数字或下划线。

WMI 客户端应用程序可以访问驱动程序的 WMI 类名称并将其显示给用户。 描述性类名称有助于使类更直观地使用。

WMI 类名在 WMI 命名空间中必须是唯一的。 因此，驱动程序的 WMI 类名称不能重复由其他驱动程序定义的名称。

为了帮助防止名称冲突，驱动程序编写器可以定义驱动程序特定的基类，并从该基类派生驱动程序的所有 WMI 类。 类名称和基类名称一起使用更有可能生成唯一名称。 例如，下面显示了串行驱动程序数据块的抽象基类：

```cpp
// Serial driver's base class for data blocks
[abstract]
class MSSerial {
}
 
// Example class definition for a data block
[
    //Class qualifiers 
]
class MSSerial_StandardSerialInformation : MSSerial 
{
    //Data items
}
```

特定于设备的自定义数据块应在基类名称中包含制造商、型号和驱动程序或设备的类型。 例如：

```cpp
[abstract]
class Adaptec1542 {
}
 
class Adaptec1542_Bandwidth : Adaptec1542 {
    //Data items
}
 
class Adaptec1542_Speed : Adaptec1542 {
    //Data items
}
```

WMI 只允许在给定的类层次结构中使用一个抽象基类。 定义事件块的类必须从 **register-wmievent** 派生而来，这是一个抽象基类，因此不能在事件块的驱动程序定义基类中使用 **抽象** 限定符。 相反，从 **register-wmievent** 派生一个非抽象基类，然后从该基类派生单个事件类。 例如：

```cpp
//Serial driver's base class for event blocks
class MSSerialEvent : WmiEvent 
{
}
 
//Example class definition for an event block
[
    //Class qualifiers 
]
class MSSerial_SendEvent : MSSerialEvent 
{
    //Data items
}
```

有关以 MOF 格式定义基类的详细信息，请参阅 Microsoft Windows SDK。

 

 




