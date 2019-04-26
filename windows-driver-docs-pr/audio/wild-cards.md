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
ms.openlocfilehash: 0634f49d3f60dec7ff690f6dd72cf29d149dfe73
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328455"
---
# <a name="wild-cards"></a>通配符


## <span id="wild_cards"></span><span id="WILD_CARDS"></span>


标头文件 Ks.h 定义的以下通配符参数[ **KS 数据范围**](https://msdn.microsoft.com/library/windows/hardware/ff561658):

-   KSDATAFORMAT\_TYPE\_WILDCARD

-   KSDATAFORMAT\_SUBTYPE\_WILDCARD

-   KSDATAFORMAT\_SPECIFIER\_WILDCARD

**MajorFormat**，**子格式**，并**说明符**的成员**DataRange**隶属[ **KSDATARANGE\_音频**](https://msdn.microsoft.com/library/windows/hardware/ff537096)结构可以设置为这些值。 通配符匹配任何对应到它被比较的值，包括可能在将来定义任何数据格式。 可以将数据移动而无需了解的数据格式的系统筛选器是通配符的主要用户。 适配器驱动程序应避免在其筛选器的 pin，数据区域中指定通配符，但它们应准备好接受客户端筛选器的 pin 的数据范围中的通配符。

 

 




