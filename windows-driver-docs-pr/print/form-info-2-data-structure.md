---
title: FORM_INFO_2 数据结构
description: FORM_INFO_2 数据结构
keywords:
- FORM_INFO_2 数据结构 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 841cc5351a34cc278871248dc0efdf3f275fef40
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797067"
---
# <a name="form_info_2-data-structure"></a>窗体 \_ 信息 \_ 2 数据结构


在 Windows Vista 中，打印后台处理程序和 Unidrv 打印机驱动程序已增强，可以在多语言环境中提供更好的支持。 后台处理程序支持多语言用户界面 (MUI) 字符串形式的窗体显示名称和新的表单 \_ 信息 \_ 2 数据结构，以包含支持 MUI 字符串所需的其他信息。

按 \_ 如下所 \_ 示定义表单 INFO 1 数据结构。

```cpp
typedef struct _FORM_INFO_1 { 
  DWORD  Flags; 
  LPTSTR  pName; 
  SIZEL   Size; 
  RECTL   ImageableArea; 
} FORM_INFO_1, *PFORM_INFO_1;
```

在窗体 \_ 信息 \_ 1 中，pName 成员是唯一的字符串字段，因此你可以使用它来创建内部搜索例程用于在内部数据库中查找表单的键名称，以及显示给最终用户的显示名称。

下面的 \_ \_ 代码示例中定义的窗体 INFO 2 结构添加了其他字段以提供 MUI 支持。

```cpp
typedef struct _FORM_INFO_2 { 
  DWORD    Flags; 
  LPTSTR   pName; 
  SIZEL    Size; 
  RECTL    ImageableArea;
  LPCSTR   pKeyword;
  DWORD    StringType;
  LPCTSTR  pMuiDll;
  DWORD    dwResourceId;
  LPCTSTR  pDisplayName;
  LANGID   wLangId; 
} FORM_INFO_2, *PFORM_INFO_2;
```

表单 \_ 信息 \_ 2 添加了 pKeyword 成员，以允许添加 distinct 关键字，该关键字可以与显示名称不同。

此结构还允许您通过使用 pMuiDll 和 dwResourceId 成员将资源 DLL 和资源 ID 添加到窗体数据库中。 当 StringType 成员具有 STRING MUIDLL 的值 \_ ，并且 pMuiDll 和 dwResourceId 成员包含资源 DLL 和显示名称的标识符时，后台处理程序中的 **AddForm** 函数将在 DLL 中查找显示名称，并在内部记录该名称。 如果调用 GetForm 或 EnumForms 函数的级别值为2，则在表单 INFO 2 结构中返回的信息 \_ \_ 将包含 pDisplayName 引用的显示名称和 wLangID 中的相应语言 ID。

在调用 AddForm 时，继续使用窗体 INFO 1 结构的打印机驱动程序 \_ \_ 将仅存储在 forms 数据库的该结构中找到的信息。 \_ \_ \_ \_ 当通过调用 GetForm 或 EnumForms （返回窗体 **NULL** \_ info 2 结构）进行查询时，窗体 info 2 结构中找不到的成员将为 NULL 或 0 \_ 。

有关添加打印机窗体以及如何使用窗体 \_ 信息 \_ 1 和窗体 \_ 信息 \_ 2 数据结构的详细信息，请参阅 Microsoft Windows SDK 文档。

 

 




