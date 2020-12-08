---
title: 能否在跟踪代码中使用枚举
description: 能否在跟踪代码中使用枚举
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3dfbc4d61aedc60c26f5bf76799ba477bbf5bb5d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791567"
---
# <a name="can-i-use-enumerations-in-my-tracing-code"></a>是否可以在跟踪代码中使用枚举？


您可以使用枚举在跟踪消息中显示有意义的字词，而不是显示用户必须解码的整数值。

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

若要在跟踪消息中使用枚举，请将以下配置数据添加到源文件中。 此代码指示 WPP 提取枚举的符号信息，并使用在显示枚举记录值时定义的名称。

```
// begin_wpp config 
// CUSTOM_TYPE(dayset, ItemEnum(_wday) );
// end_wpp
```

然后，可以在跟踪消息的格式字符串中使用 **dayset** 自定义类型。 例如：

```
 _wday p = wednesday;

 DoTraceMessage(NOISE " %!dayset!", p);
```

最后，由于你将配置数据添加到非配置文件 (文件) 而不是 .ini 文件，因此，请将 **-scan** 参数添加到 \_ 调用 wpp 预处理器的 RUN WPP 宏。 这会通知 WPP 查找指定文件中的配置数据。 例如：

```
RUN_WPP -scan:trace.c
```









