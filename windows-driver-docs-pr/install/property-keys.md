---
title: 属性键
description: 属性键
ms.assetid: 767dbe79-72c6-4445-8d4a-8be53a080825
keywords:
- 设备属性 WDK 设备安装，属性键
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef08289fb67aa8312a2b29b85fda7615f049ec79
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325745"
---
# <a name="property-keys"></a>属性键


以编程方式，所有设备中的属性[统一的设备属性模型](unified-device-property-model--windows-vista-and-later-.md)由属性键。 属性键在编码时[ **DEVPROPKEY** ](https://msdn.microsoft.com/library/windows/hardware/ff543544)结构。 在定义属性键*Devpkey.h*。

DEVPROPKEY 结构具有以下成员：

<a href="" id="fmtid"></a>**fmtid**  
标识的属性类别的 DEVPROPGUID 类型的变量。

<a href="" id="pid"></a>**pid**  
DEVPROPID 类型的变量的属性标识符。 内部系统方面的考虑，属性标识符必须大于或等于 2。

若要创建自定义设备属性，请使用[ **DEFINE_DEVPROPKEY** ](https://msdn.microsoft.com/library/windows/hardware/ff541072)宏。

下面是如何使用 DEFINE_DEVPROPKEY 宏创建 DEVPROPKEY 结构的示例。 结构的名称是"DEVPROPKEYStructureName"、 值通过 0xe0 0xde5c254e 序列提供的 GUID 值，和"2"的值是属性标识符。

```cpp
DEFINE_DEVPROPKEY(DEVPROPKEYStuctureName, 0xde5c254e, 0xab1c, 0xeffd, 0x80, 0x20, 0x67, 0xd1, 0x46, 0xa8, 0x50, 0xe0, 2)
```

**请注意**  保留仅供系统使用的系统定义的属性键类别。

 

 

 





