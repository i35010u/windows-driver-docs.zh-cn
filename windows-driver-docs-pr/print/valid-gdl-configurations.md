---
title: 有效 GDL 配置
description: 有效 GDL 配置
ms.assetid: 68dbe7f7-4f6d-46e5-b2f1-27b123c4bedb
keywords:
- GDL WDK 配置
- 分析器 WDK GDL，验证配置
- 配置 WDK GDL，有效的配置
- 验证 GDL 配置 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 001d71ea7dd73e6303894488457410d8a66259ed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541219"
---
# <a name="valid-gdl-configurations"></a>有效 GDL 配置


GDL 分析器接口函数将始终验证传入的配置，因为分析器将假定客户端有时可能有误，提供无效的配置。 有关无效配置的详细信息，请参阅[使用无效 GDL 配置](using-invalid-gdl-configurations.md)。

有效的配置满足以下条件：

-   配置包含 GDL 中定义每个参数的条目。

-   配置不包含条目 GDL 中未定义的参数。

-   每个分配给参数的值由定义\*选项构造为该参数。

-   PICKONE 参数具有一个且只有一个分配的值。

-   PICKMANY 参数具有分配至少一个值。

若要避免由于分析器的验证过程而丢失您的配置的意图，应将有效的配置传递给分析器函数。

 

 




