---
title: WMI 类名和基类
description: WMI 类名和基类
ms.assetid: 6c3f74a3-e596-4694-8619-db38d67e030c
keywords:
- 基类 WDK WMI
- 名称 WDK WMI
- WDK WMI 类
- WMI WDK 内核类
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ff351f5606a65786c69fb4b635229e30dd5c581
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380927"
---
# <a name="wmi-class-names-and-base-classes"></a>WMI 类名和基类





WMI 类名不区分大小写，必须以字母开头并且不能开始或结尾下划线。 所有剩余的字符必须是字母、 数字或下划线。

WMI 客户端应用程序可以访问驱动程序的 WMI 类名，并向用户显示它们。 描述性类名称可帮助使类使用更加直观。

WMI 类名称必须是唯一的 WMI 命名空间中。 因此驱动程序的 WMI 类名不能重复那些由另一个驱动程序定义。

若要防止名称冲突，驱动程序编写器可以定义特定于驱动程序的基类，并从该基类派生的所有驱动程序的 WMI 类。 类名和基类名称一起构成了更有可能产生的唯一名称。 例如，下面显示了串行驱动程序的数据块的抽象基类：

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

特定于设备的自定义数据块应包括制造商、 型号和类型的驱动程序或设备中的基类名称。 例如：

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

WMI 允许给定的类层次结构中只有一个抽象基类。 定义事件块的类必须派生自**WmiEvent**，这是一个抽象基类，因此**抽象**限定符不能在中使用的驱动程序定义的基类的事件块。 相反，派生从非抽象基类**WmiEvent**，然后从该基类派生单个事件的类。 例如：

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

有关 MOF 格式定义基类，这些类的详细信息，请参阅 Microsoft Windows SDK。

 

 




