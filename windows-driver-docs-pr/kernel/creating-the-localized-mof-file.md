---
title: 创建本地化的 MOF 文件
description: 创建本地化的 MOF 文件
ms.assetid: 1cc99e43-b09a-445d-abb6-4a3d73b6d7ed
keywords:
- MOF 文件 WDK WMI
- 本地化 MOF 文件
- 属性限定符 WDK WMI
- 已修正的 WDK WMI 类
- 多个 MOF 文件 WDK WMI
- 语言 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9585b6a44f07154a7a09ed41c19c3a0ba713a43a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541527"
---
# <a name="creating-the-localized-mof-file"></a>创建本地化的 MOF 文件





在 Windows XP 和更高版本的操作系统，驱动程序 WMI 架构本地化，从而*已修正*版本的每个类。 类是修改的版更新依赖于区域设置的属性限定符。

类是修改的版具有与类声明中，前面有相同的格式**修正合同**限定符。 已修正的类声明还包括<strong>区域设置 (</strong>0x<em>XXX</em>**)** 限定符，其中*XXX*指定区域设置标识符 (LCID)区域设置。

已修正的声明包含已修改的属性声明。 具有每个本地化的属性限定符 **： 已修正**修饰符附加到它。 例如，本地化的版本的**说明 ("**<em>描述字符串</em>**")** 会**说明 ("** <em>本地化描述字符串</em>**"): 已修正**。

下面是声明的基本类后, 跟其针对美国英语的修正合同的示例。

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

仅已修改的属性必须包含已修正的类中。 类和属性名称不能进行本地化。 仅属性限定符可以进行本地化。

本地化的类包含原始类的命名空间的子命名空间进行组织。 以毫秒为单位找到给定区域设置的类\_*XXX*子命名空间，其中*XXX*表示十六进制对该区域设置 LCID。 例如，驱动程序位于\\根\\默认情况下的 wmi 命名空间。 在中找到已修正的类，针对美式英语，本地化\\根\\wmi\\MS\_409 命名空间。

有关 WMI 本地化的详细信息，请参阅[WMI 国际支持](https://go.microsoft.com/fwlink/p/?linkid=8774)网站。

 

 




