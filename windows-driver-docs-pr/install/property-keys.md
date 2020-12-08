---
title: 属性键
description: 属性键
keywords:
- 设备属性 WDK 设备安装，属性密钥
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 852cafbc359cc431a9762d0abfa036bdbf88bcf9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796031"
---
# <a name="property-keys"></a>属性键


以编程方式， [统一设备属性模型](unified-device-property-model--windows-vista-and-later-.md) 中的所有设备属性都由属性键表示。 属性键被编码为 [**DEVPROPKEY**](./devpropkey.md) 结构。 属性键在 *Devpkey* 中定义。

DEVPROPKEY 结构包含以下成员：

<a href="" id="fmtid"></a>**fmtid**  
标识属性类别的 DEVPROPGUID 类型的变量。

<a href="" id="pid"></a>**p&id**  
作为属性标识符的 DEVPROPID 类型的变量。 由于内部系统原因，属性标识符必须大于或等于2。

若要创建自定义设备属性键，请使用 [**DEFINE_DEVPROPKEY**](./define-devpropkey.md) 宏。

下面的示例演示如何使用 DEFINE_DEVPROPKEY 宏创建 DEVPROPKEY 结构。 结构的名称为 "DEVPROPKEYStructureName"，值序列0xde5c254e 到0xe0 提供 GUID 值，值 "2" 是属性标识符。

```cpp
DEFINE_DEVPROPKEY(DEVPROPKEYStuctureName, 0xde5c254e, 0xab1c, 0xeffd, 0x80, 0x20, 0x67, 0xd1, 0x46, 0xa8, 0x50, 0xe0, 2)
```

**注意**   系统定义的属性键类别只保留供系统使用。

 

 

