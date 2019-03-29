---
title: 定义自定义属性
description: 定义自定义属性
ms.assetid: c3b69482-12ad-4b9f-8c0c-5ce315032d51
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0926f362cde777d51dc12336a2ea92d97380f110
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562116"
---
# <a name="defining-custom-properties"></a>定义自定义属性





如有必要为 WIA 微型驱动程序来定义自定义属性，WIA\_私有\_DEVPROP 属性应该用于自定义根项属性和 WIA\_专用\_ITEMPROP 属性应为用于其他项属性。 这些常量中定义*wiadef.h*。

下面的代码示例显示了三个根项属性的定义。 第一个自定义根项属性，自定义的属性 ID\_根\_PROP\_1，定义根据 WIA\_专用\_DEVPROP。 更多的根项属性的属性 Id 定义根据 WIA\_私有\_DEVPROP + 1，WIA\_专用\_DEVPROP + 2，依此类推。 如果需要更多的自定义根项属性，可以继续该模式。

```cpp
#define CUSTOM_ROOT_PROP_1 WIA_PRIVATE_DEVPROP
#define CUSTOM_ROOT_PROP_2 (WIA_PRIVATE_DEVPROP + 1) 
#define CUSTOM_ROOT_PROP_3 (WIA_PRIVATE_DEVPROP + 2) 
```

下面的示例演示三个自定义子项目属性和属性 Id 的定义。 第一个自定义子项属性，自定义的属性 ID\_子\_PROP\_1，定义根据 WIA\_专用\_ITEMPROP。 另一个子项目属性的属性 Id 定义根据 WIA\_专用\_ITEMPROP + 1，依此类推。 为之前，该模式可以继续如果需要这些自定义子项目属性的详细信息。

```cpp
#define CUSTOM_CHILD_PROP_1 WIA_PRIVATE_ITEMPROP
#define CUSTOM_CHILD_PROP_2 (WIA_PRIVATE_ITEMPROP + 1) 
#define CUSTOM_CHILD_PROP_3 (WIA_PRIVATE_ITEMPROP + 2)
```

自定义 WIA 属性必须与自定义属性 Id 关联的自定义属性名称。 下面的代码示例显示了三个自定义根项属性名称的定义。 (这些属性名称用于自定义的属性 Id 创建在上一示例中，其中自定义属性名称包含在自定义\_根\_PROP\_1\_STR 程序与自定义根项属性 ID 自定义\_根\_PROP\_1。)

```cpp
#define CUSTOM_ROOT_PROP_1_STR L"My First Custom Root Item Property"
#define CUSTOM_ROOT_PROP_2_STR L"My Second Custom Root Item Property"
#define CUSTOM_ROOT_PROP_3_STR L"My Third Custom Root Item Property"
```

**请注意**   WIA 属性名称均*不*本地化为多种语言。 这是因为可以通过使用属性 ID 或属性名称的应用程序读取 WIA 属性。 如果使用的名称，它必须是常量，就像 ID 的属性。
