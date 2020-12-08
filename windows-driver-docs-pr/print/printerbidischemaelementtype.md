---
title: PRINTERBIDISCHEMAELEMENTTYPE 枚举
description: 指定在双向操作中传输的数据的可能值。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- PRINTERBIDISCHEMAELEMENTTYPE 枚举打印设备
topic_type:
- apiref
api_name:
- PRINTERBIDISCHEMAELEMENTTYPE
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c168a355e2cc50f84ebb88748e8690756a991baf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807227"
---
# <a name="printerbidischemaelementtype-enumeration"></a>PRINTERBIDISCHEMAELEMENTTYPE 枚举

指定在双向操作中传输的数据的可能值

<a name="syntax"></a>语法
------

```cpp
typedef enum _PRINTERBIDISCHEMAELEMENTTYPE { 
  PrinterBidiSchemaElementType_Null    = 0,
  PrinterBidiSchemaElementType_Int     = 1,
  PrinterBidiSchemaElementType_Float   = 2,
  PrinterBidiSchemaElementType_Bool    = 3,
  PrinterBidiSchemaElementType_String  = 4,
  PrinterBidiSchemaElementType_Text    = 5,
  PrinterBidiSchemaElementType_Enum    = 6,
  PrinterBidiSchemaElementType_Blob    = 7
} PRINTERBIDISCHEMAELEMENTTYPE;
```

<a name="constants"></a>常量
---------

**PrinterBidiSchemaElementType \_ Null**  
无数据。

**PrinterBidiSchemaElementType \_ Int**  
Data 是整数。

**PrinterBidiSchemaElementType \_ Float**  
数据是浮点数。

**PrinterBidiSchemaElementType \_ Bool**  
Data 为布尔值。

**PrinterBidiSchemaElementType \_ 字符串**  
Data 是 Unicode 字符串。

**PrinterBidiSchemaElementType \_ 文本**  
数据是不可本地化的 Unicode 字符串。

**PrinterBidiSchemaElementType \_ 枚举**  
Data 是 Unicode 字符串。

**PrinterBidiSchemaElementType \_ Blob**  
数据为二进制数据。

## <a name="see-also"></a>请参阅

[**BidiType**](iprinterbidischemaelement-biditype.md)
