---
title: 通配符
description: 通配符
ms.assetid: fc42fb2d-8df9-47d6-9034-c0588ee81c95
keywords:
- 数据交集处理程序 WDK 音频，通配符
- 通配符 WDK 音频
- 数据范围 WDK 音频，通配符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c189459c4312453621a9bab2fe3b39f72e9f87a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206625"
---
# <a name="wild-cards"></a>通配符


## <span id="wild_cards"></span><span id="WILD_CARDS"></span>


标头文件 Ks 定义了用于 [**Ks 数据范围**](/previous-versions/ff561658(v=vs.85))的下列通配符参数：

-   KSDATAFORMAT \_ 类型 \_ 通配符

-   KSDATAFORMAT \_ 子类型 \_ 通配符

-   KSDATAFORMAT \_ 说明符 \_ 通配符

[**KSDATARANGE \_ 音频**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)结构的**DataRange**成员的**MajorFormat**、 **Subformat**和**说明符**成员可设置为这些值。 通配符与所比较的任何相应值（包括将来可能定义的任何数据格式）匹配。 无需了解数据格式即可移动数据的系统筛选器是通配符的主要用户。 适配器驱动程序应避免在数据区域中为其筛选器引脚指定通配符，但应准备好在客户端筛选器的 pin 的数据范围内接受通配符。

 

