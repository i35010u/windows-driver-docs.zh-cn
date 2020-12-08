---
title: 定义自定义属性
description: 定义自定义属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98d944cd76e8bf788e6ba1f4cd3e672604932b4b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813779"
---
# <a name="defining-custom-properties"></a>定义自定义属性





如果 WIA 微型驱动程序定义自定义属性是必需的，则应将 WIA \_ private \_ DEVPROP 属性用于自定义根项属性，并将 wia \_ private \_ ITEMPROP 属性用于其他项属性。 这些常量在 *wiadef* 中定义。

下面的示例代码演示了三个根项属性的定义。 第一个自定义根项属性的属性 ID （自定义 \_ 根属性 \_ \_ 1）是根据 WIA \_ PRIVATE DEVPROP 定义的 \_ 。 其他根项属性的属性 Id 定义为 WIA \_ private \_ DEVPROP + 1、wia \_ private \_ DEVPROP + 2，等等。 如果需要其他自定义根项属性，则可以继续此模式。

```cpp
#define CUSTOM_ROOT_PROP_1 WIA_PRIVATE_DEVPROP
#define CUSTOM_ROOT_PROP_2 (WIA_PRIVATE_DEVPROP + 1) 
#define CUSTOM_ROOT_PROP_3 (WIA_PRIVATE_DEVPROP + 2) 
```

下一个示例显示了三个自定义子项目属性和属性 Id 的定义。 自定义子项目属性 "自定义子属性 1" 的属性 ID \_ \_ \_ 是根据 WIA PRIVATE ITEMPROP 定义的 \_ \_ 。 其他子级项属性的属性 Id 是根据 WIA \_ PRIVATE \_ ITEMPROP + 1，依此类推。 与前面一样，如果需要更多的自定义子项目属性，模式可以继续。

```cpp
#define CUSTOM_CHILD_PROP_1 WIA_PRIVATE_ITEMPROP
#define CUSTOM_CHILD_PROP_2 (WIA_PRIVATE_ITEMPROP + 1) 
#define CUSTOM_CHILD_PROP_3 (WIA_PRIVATE_ITEMPROP + 2)
```

自定义 WIA 属性必须具有与自定义属性 Id 关联的自定义属性名称。 下面的示例代码演示三个自定义根项属性名称的定义。  (这些属性名称与在上一个示例中创建的自定义属性 Id 一起使用，其中自定义根属性 1 STR 中包含的自定义属性名称 \_ \_ \_ \_ 与自定义根项属性 ID 自定义根属性1相关联 \_ \_ \_ 。 ) 

```cpp
#define CUSTOM_ROOT_PROP_1_STR L"My First Custom Root Item Property"
#define CUSTOM_ROOT_PROP_2_STR L"My Second Custom Root Item Property"
#define CUSTOM_ROOT_PROP_3_STR L"My Third Custom Root Item Property"
```

**注意**   WIA 属性名称 *未* 采用多种语言进行本地化。 这是因为使用属性 ID 或属性名称的应用程序可以读取 WIA 属性。 如果使用该名称，则它必须是常量，就像属性 ID 为一样。
