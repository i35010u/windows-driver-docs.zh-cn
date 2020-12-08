---
title: 已本地化字符串的 [String] 部分更改
description: 这项 INF 要求确保伪本地化的生成正常运行。 要求是将可本地化的字符串与非本地化字符串的字符串部分进行描绘
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3596ff1481680777eb59af970106efe27fba7be4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810601"
---
# <a name="string-section-changes-for-localized-strings"></a>\[\]本地化字符串的字符串部分更改


这项 INF 要求确保伪本地化的生成正常运行。 要求是将可本地化的字符串与字符串部分中的不可本地化的字符串进行界定。

下面的示例没有已本地化或未本地化的的前言;不应使用此内容：

``` syntax
[Strings]

REG_MULTI_SZ   = 0x00010000
REG_DWORD      = 0x00010001

MSFT = "Microsoft"
IHV  = "Contoso, Ltd"
```

应改为使用以下示例：注意新行：

``` syntax
[Strings]

;Localizable
MSFT = "Microsoft"
IHV  = "Contoso, Ltd"


;Non-Localizable
REG_MULTI_SZ   = 0x00010000
REG_DWORD      = 0x00010001
```

 

 





