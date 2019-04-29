---
title: PRINTERBIDISCHEMAELEMENTTYPE 枚举
description: 指定在双向操作中传输的数据的可能值。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 18F2325D-DA22-4D73-8560-62FDEF1E04A8
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
ms.openlocfilehash: f6958248a166aa14b697c6db663230cef1385207
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390274"
---
# <a name="printerbidischemaelementtype-enumeration"></a>PRINTERBIDISCHEMAELEMENTTYPE 枚举

指定在双向操作中传输的数据的可能值

<a name="syntax"></a>语法
------

```cpp
typedef enum _PRINTERBIDISCHEMAELEMENTTYPE { 
  PrinterBidiSchemaElementType_Null    = 0,
  PrinterBidiSchemaElementType_Int     = 1,
  PrinterBidiSchemaElementType_Float   = 2,
  PrinterBidiSchemaElementType_Bool    = 3,
  PrinterBidiSchemaElementType_String  = 4,
  PrinterBidiSchemaElementType_Text    = 5,
  PrinterBidiSchemaElementType_Enum    = 6,
  PrinterBidiSchemaElementType_Blob    = 7
} PRINTERBIDISCHEMAELEMENTTYPE;
```

<a name="constants"></a>常量
---------

**PrinterBidiSchemaElementType\_Null**  
没有数据。

**PrinterBidiSchemaElementType\_Int**  
数据是一个整数。

**PrinterBidiSchemaElementType\_Float**  
数据是浮点数。

**PrinterBidiSchemaElementType\_Bool**  
数据是一个布尔值。

**PrinterBidiSchemaElementType\_String**  
数据是 Unicode 字符的字符串。

**PrinterBidiSchemaElementType\_Text**  
数据是不可本地化的 Unicode 字符串。

**PrinterBidiSchemaElementType\_Enum**  
数据是 Unicode 字符串。

**PrinterBidiSchemaElementType\_Blob**  
数据是二进制数据。

## <a name="see-also"></a>请参阅

[**BidiType**](iprinterbidischemaelement-biditype.md)
