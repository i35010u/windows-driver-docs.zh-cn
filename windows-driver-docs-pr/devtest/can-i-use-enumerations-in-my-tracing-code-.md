---
title: 可以在我的跟踪代码中使用枚举
description: 可以在我的跟踪代码中使用枚举
ms.assetid: c42ab1ad-6b8f-458f-ba29-e3553095c853
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 098abf6d7e5374b7e165beb3b82f59bf1ead41b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544079"
---
# <a name="can-i-use-enumerations-in-my-tracing-code"></a>可以在我的跟踪代码中使用枚举？


枚举可用于跟踪消息，而不是显示用户必须进行解码的整数值中显示有意义的术语。

例如，在代码中定义以下枚举：

```
#define SPECIALDAY  0xF0000000
enum _wday {
  sunday = 0,
  monday = 55,
  tuesday = 3,
  wednesday = 1 | SPECIALDAY  ,
  thursday =  7 | SPECIALDAY,
  friday =  5,
  saturday = 6
};
```

若要在跟踪消息中使用枚举，请将以下配置数据添加到源文件。 此代码将定向 WPP 来提取枚举的符号信息和使用已定义显示在枚举时的名称记录的值。

```
// begin_wpp config 
// CUSTOM_TYPE(dayset, ItemEnum(_wday) );
// end_wpp
```

然后，可以使用**dayset**的跟踪消息的格式字符串中的自定义类型。 例如：

```
 _wday p = wednesday;

 DoTraceMessage(NOISE " %!dayset!", p);
```

最后，因为配置数据添加到非配置文件 （.ini 文件之外的文件） 中，添加 **-扫描**参数运行\_WPP 宏调用 WPP 预处理器。 这会通知 WPP 查找配置数据中指定的文件。 例如：

```
RUN_WPP -scan:trace.c
```









