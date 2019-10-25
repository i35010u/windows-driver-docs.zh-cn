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
ms.openlocfilehash: eb498da0e0a00515aacab32141829e5a333209cf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832232"
---
# <a name="wild-cards"></a>通配符


## <span id="wild_cards"></span><span id="WILD_CARDS"></span>


标头文件 Ks 定义了用于[**Ks 数据范围**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))的下列通配符参数：

-   KSDATAFORMAT\_键入\_通配符

-   KSDATAFORMAT\_子类型\_通配符

-   KSDATAFORMAT\_说明符\_通配符

[**KSDATARANGE\_音频**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)结构的**DataRange**成员的**MajorFormat**、 **Subformat**和**说明符**成员可设置为这些值。 通配符与所比较的任何相应值（包括将来可能定义的任何数据格式）匹配。 无需了解数据格式即可移动数据的系统筛选器是通配符的主要用户。 适配器驱动程序应避免在数据区域中为其筛选器引脚指定通配符，但应准备好在客户端筛选器的 pin 的数据范围内接受通配符。

 

 




