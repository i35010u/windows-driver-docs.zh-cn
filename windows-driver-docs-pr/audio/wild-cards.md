---
title: 通配符
description: 通配符
ms.assetid: fc42fb2d-8df9-47d6-9034-c0588ee81c95
keywords:
- 数据交集处理程序 WDK 音频，通配符
- 通配符 WDK 音频
- 数据范围 WDK 音频通配符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16a31972735db8493c7d3769daae721f9a702951
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364783"
---
# <a name="wild-cards"></a>通配符


## <span id="wild_cards"></span><span id="WILD_CARDS"></span>


标头文件 Ks.h 定义的以下通配符参数[ **KS 数据范围**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85)):

-   KSDATAFORMAT\_TYPE\_WILDCARD

-   KSDATAFORMAT\_SUBTYPE\_WILDCARD

-   KSDATAFORMAT\_SPECIFIER\_WILDCARD

**MajorFormat**，**子格式**，并**说明符**的成员**DataRange**隶属[ **KSDATARANGE\_音频**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdatarange_audio)结构可以设置为这些值。 通配符匹配任何对应到它被比较的值，包括可能在将来定义任何数据格式。 可以将数据移动而无需了解的数据格式的系统筛选器是通配符的主要用户。 适配器驱动程序应避免在其筛选器的 pin，数据区域中指定通配符，但它们应准备好接受客户端筛选器的 pin 的数据范围中的通配符。

 

 




