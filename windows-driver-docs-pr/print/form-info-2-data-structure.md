---
title: FORM_INFO_2 数据结构
description: FORM_INFO_2 数据结构
ms.assetid: df953fe9-00a2-468a-a2ae-ba8f3fce9982
keywords:
- FORM_INFO_2 数据结构 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3d175c3ba4212fc0382702b3d31855c78bd2511
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564045"
---
# <a name="forminfo2-data-structure"></a>窗体\_信息\_2 个数据结构


打印后台处理程序和 Unidrv 打印机驱动程序已得到增强，在 Windows Vista 中提供更好地支持多语言环境中的打印机表单。 后台处理程序支持多语言用户界面 (MUI) 字符串的窗体的显示名称和新的窗体\_信息\_2 个数据结构，以包括你需要支持 MUI 字符串的附加信息。

在窗体\_信息\_1 的数据结构定义，如下所示。

```cpp
typedef struct _FORM_INFO_1 { 
  DWORD  Flags; 
  LPTSTR  pName; 
  SIZEL   Size; 
  RECTL   ImageableArea; 
} FORM_INFO_1, *PFORM_INFO_1;
```

在窗体\_信息\_1，pName 成员是唯一的字符串字段，因此可以使用它来创建向最终用户显示内部搜索例程使用内部数据库中查找窗体并也可用作显示名称的项名称。

在窗体\_信息\_2 结构，其定义在下面的代码示例中，将添加其他字段，提供的 MUI 支持。

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

窗体\_信息\_2 添加 pKeyword 成员，使添加 distinct 关键字，也可能不同于的显示名称。

此结构还可以使用 pMuiDll 和 dwResourceId 成员添加到窗体数据库的资源 DLL 和资源 ID。 如果 StringType 成员的字符串的值\_MUIDLL 和 pMuiDll 和 dwResourceId 成员包含的资源 DLL 和显示名称的标识符**AddForm**函数在后台处理程序中的查找的显示在 DLL 中的名称，并在内部记录。 GetForm 或 EnumForms 函数级别值为 2，则在窗体中返回的信息的调用时\_信息\_2 结构将包含 pDisplayName 引用，并相应语言 ID 中的显示名称wLangID。

继续使用窗体的打印机驱动程序\_信息\_1 结构时它们调用 AddForm 将存储仅在窗体数据库中该结构中找到的信息。 窗体中的成员\_INFO\_窗体中找不到 2 个结构\_信息\_1 结构将是**NULL**或 0 对 GetForm 或 EnumForms 返回窗体的调用进行查询时\_信息\_2 结构。

有关添加打印机纸张规格以及使用窗体的详细信息\_INFO\_1 和窗体\_信息\_2 个数据结构，请参阅 Microsoft Windows SDK 文档。

 

 




