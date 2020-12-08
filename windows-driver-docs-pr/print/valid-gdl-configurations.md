---
title: 有效的 GDL 配置
description: 有效的 GDL 配置
keywords:
- GDL WDK，配置
- 分析器 WDK GDL，验证配置
- 配置 WDK GDL，有效配置
- 验证 GDL 配置 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d66fd71ee8568883ac55582ca56b97d1114af092
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785863"
---
# <a name="valid-gdl-configurations"></a>有效的 GDL 配置


GDL 分析器接口函数将始终验证传入配置，因为分析程序假定客户端有时可能会出错，并为其提供无效的配置。 有关无效配置的详细信息，请参阅 [使用无效的 GDL 配置](using-invalid-gdl-configurations.md)。

有效配置满足以下条件：

-   此配置包含 GDL 中定义的每个参数的条目。

-   该配置不包含 GDL 中未定义的参数的条目。

-   分配给参数的每个值由 \* 该参数的选项构造定义。

-   PICKONE 参数有一个且仅有一个值被分配。

-   PICKMANY 参数至少分配了一个值。

为了防止因分析器的验证过程而导致配置不会丢失，应将有效配置传递到分析器函数。

 

 




