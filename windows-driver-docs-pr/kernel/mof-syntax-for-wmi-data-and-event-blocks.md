---
title: WMI 数据和事件块的 MOF 语法
description: WMI 数据和事件块的 MOF 语法
keywords:
- WMI WDK 内核，事件块
- 事件块 WDK WMI
- 数据块 WDK WMI
- WMI WDK 内核，数据块
- 阻止 WDK WMI
- MOF 文件 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 068b281ff94fc27b0230ffa64f42039d3e45469d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838015"
---
# <a name="mof-syntax-for-wmi-data-and-event-blocks"></a>WMI 数据和事件块的 MOF 语法





驱动程序的 WMI 架构描述了其数据块，这些数据块定义驱动程序可以提供的信息以及它可以在响应 WMI 请求时执行的方法。 驱动程序的架构还描述了其事件块，即当发生驱动程序确定的事件（WMI 客户端用户请求通知）时，驱动程序将这些数据块发送到 WMI。

驱动程序编写器在托管对象格式 (MOF) 中定义驱动程序的架构。 MOF 是由桌面管理任务组 (DMTF) 创建的已编译语言，并基于接口定义语言 (IDL) 。 驱动程序的 MOF 文件包含驱动程序向 WMI 公开的每个数据块和事件块的 MOF 类定义。

WMI 数据块的 MOF 类定义采用以下语法：

```mof
[Required and optional class qualifiers]

classClassName : OptionalBaseClass 
{ 
[key, read] 
string InstanceName; 
[read] 
boolean Active; 
[ Required and optional property qualifiers ] 
datatype itemname1; 
[ Required and optional property qualifiers ] 
datatype itemnameN; 
}; 
```

以下主题介绍上述语法元素：

[WMI 类限定符](wmi-class-qualifiers.md)

[WMI 类名和基类](wmi-class-names-and-base-classes.md)

[WMI 类中的必需项](required-items-in-wmi-classes.md)

[WMI 属性限定符](wmi-property-qualifiers.md)

[驱动程序定义的 WMI 数据项](driver-defined-wmi-data-items.md)

[WMI 类示例](wmi-class-examples.md)

有关适用于 WMI 客户端和其他类型的应用程序的 MOF 语法的一般讨论，请参阅 Microsoft Windows SDK。

 

 




