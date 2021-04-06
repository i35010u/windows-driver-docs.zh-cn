---
title: 'PaddingByteInformationDisclosure (补充 Windows 驱动程序 CodeQL 查询) '
description: PaddingByteInformationDisclosure 补充 Windows Driver CodeQL 查询
ms.date: 01/11/2021
ms.localizationpriority: medium
ms.openlocfilehash: c8433fcaf4b8bc8229c4e25f624a2bb9f716842a
ms.sourcegitcommit: 0e165d26ea3887d87eb41d591b8d847038a73085
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/05/2021
ms.locfileid: "106387619"
---
# <a name="paddingbyteinformationdisclosure-windows-driver-codeql-query"></a>PaddingByteInformationDisclosure (Windows Driver CodeQL Query) 

## <a name="overview"></a>概述

如果一个新分配的结构或类包含填充字节，则该结构或类将逐个成员初始化可能会泄漏信息。

## <a name="recommendation"></a>建议

请确保已初始化结构或类中的所有填充字节。

如果可能，请使用 *memset* 来初始化整个结构/类。

## <a name="example"></a>示例

下面的示例演示了一个方案，其中，第一个和第二个元素之间的填充未初始化：

```cpp
typedef enum { Unknown = 0, Known = 1, Other = 2 } MyStructType;
struct MyStruct { MyStructType type; UINT64 id; };
MyStruct testReturn() 
{
    // BAD: Padding between the first and second elements not initialized.
    MyStruct myBadStackStruct = { Unknown };
    return myBadStackStruct;
}
```

若要更正此错误，我们将使用 *memset* 初始化所有字节：

```cpp
typedef enum { Unknown = 0, Known = 1, Other = 2 } MyStructType;
struct MyStruct { MyStructType type; UINT64 id; };
MyStruct testReturn()
{
    // GOOD: All padding bytes initialized
    MyStruct* myGoodHeapStruct = (struct MyStruct*)malloc(sizeof(struct MyStruct));
    memset(myGoodHeapStruct, 0, sizeof(struct MyStruct));
    return *myGoodHeapStruct;
}
```

## <a name="additional-details"></a>其他详细信息

此查询可在 [Microsoft GitHub CodeQL 存储库](https://github.com/microsoft/Windows-Driver-Developer-Supplemental-Tools)中找到。  有关 Windows 驱动程序开发人员如何下载和运行 CodeQL 的详细信息，请参阅 [CodeQL 和静态工具徽标测试](./static-tools-and-codeql.md) 页。
