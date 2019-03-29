---
title: 用于本地化的字符串 [string] 部分更改
description: 此 INF 要求确保伪本地化时生成的工作。 要求是描述与非可本地化的字符串中的字符串部分可本地化
ms.assetid: F0A0C309-9FA3-4941-AF35-15CD63DB25E3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c078dcd265f3e728b502c7f3d5b9c307abdee65
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569261"
---
# <a name="string-section-changes-for-localized-strings"></a>\[字符串\]部分本地化的字符串的更改


此 INF 要求确保伪本地化时生成的工作。 要求是描述可与字符串部分中的非可本地化的字符串本地化。

下面的示例具有内容已本地化或不是，没有的前缀这不应使用：

``` syntax
[Strings]

REG_MULTI_SZ   = 0x00010000
REG_DWORD      = 0x00010001

MSFT = "Microsoft"
IHV  = "Contoso, Ltd"
```

下面的示例应改用;请注意新行：

``` syntax
[Strings]

;Localizable
MSFT = "Microsoft"
IHV  = "Contoso, Ltd"


;Non-Localizable
REG_MULTI_SZ   = 0x00010000
REG_DWORD      = 0x00010001
```

 

 





