---
title: 创建本地化 MOF 文件
description: 创建本地化 MOF 文件
keywords:
- MOF 文件 WDK WMI
- 本地化 MOF 文件
- 属性限定符 WDK WMI
- 修改后的类 WDK WMI
- 多个 MOF 文件 WDK WMI
- 语言 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8fe20b091713d6c3496cc4b25a3b726c57dddc6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792827"
---
# <a name="creating-the-localized-mof-file"></a>创建本地化 MOF 文件





在 Windows XP 和更高版本的操作系统上，驱动程序通过对每个类进行 *修改* 后的版本来本地化 WMI 架构。 类的修改版本将更新依赖于区域设置的属性限定符。

类的修改版本具有与类声明相同的格式，前面带有 **修正** 限定符。 修改后的类声明还包括一个 <strong>区域设置 (</strong>0x <em>XXX</em> **)** 限定符，其中 *XXX* 指定区域设置的区域设置标识符 (LCID) 。

修改后的声明包含修改后的属性声明。 每个本地化的属性限定符都附加了 **：修改** 后的修饰符。 例如，"说明 <em>字符串</em>**" )** **(** 说明的本地化版本将是 **说明 ( "**<em>本地化的描述字符串</em>**" ) ：已修改**。

下面是基本类的声明的示例，后面是其针对美国英语的修正。

```cpp
[guid(xxxxxxxx-xxxx-xxxx-xxxxxxxxxxxx)]
class MyClass
{
    [key] sint32 KeyProp;
    string Name;
    uint64 Timestamp;
}

[amendment, locale(0x409)
 Description("Localized version of MyClass for American English"):amended]

class MyClass
{
    [DisplayName("Key Property"):amended,
     Description("The description of KeyProp"):amended]
    sint32 KeyProp;

    [DisplayName("User Name"):amended,
     Description("The description of Name"):amended]
    string Name;
}
```

只有已修改的属性需要包含在修改后的类中。 类和属性名称不能本地化。 只能对属性限定符进行本地化。

本地化类组织在包含原始类的命名空间的子命名空间中。 给定区域设置的类可在 MS \_ *XXX* 子命名空间中找到，其中 *XXX* 表示该区域设置的十六进制 LCID。 例如，默认情况下，驱动程序位于 \\ 根 \\ wmi 命名空间中。 在 \\ 根 \\ wmi \\ MS \_ 409 命名空间中，已修改的类（为美国英语进行了本地化）。


 

 




