---
title: C28644
description: 警告不会检查 DPA_InsertPtr C28644 返回值。
ms.assetid: F145330F-E597-405F-935E-B12D65F64DDB
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28644
ms.openlocfilehash: 74e023688e5c4d42b9c7d1a66a38bfb16fedc565
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525978"
---
# <a name="c28644"></a>C28644


警告 C28644:返回值从 DPA\_InsertPtr 不检查

此警告表明内存可能会泄露。

多数调用都会[ **DPA\_InsertPtr** ](https://msdn.microsoft.com/library/windows/desktop/bb775625)函数使用在堆上分配的变量。 函数然后使用 DPA 和释放 DPA 中存储的所有对象。 当**DPA\_InsertPtr**失败，无法再进行分配的对象释放 DPA 清理代码，因此的调用方**DPA\_InsertPtr**需要释放的内存。 请注意，在调用**CleanupDPA**在下面的示例。 如果你的代码不会释放分配的对象中的方式类似于**CleanupDPA**可能不需要修复任何问题。 此缺陷假定我们要依赖于 DPA 来跟踪我们需要更高版本可用的所有对象。

下面的代码示例将生成此警告：

```
void Func()
{
    WCHAR*pszBuf=newWCHAR[MAX_PATH];
    DPA_InsertPtr(_hdpa, DA_LAST, pszBuf);
}

void CleanupDPA()
{
    int count = DPA_GetCount(_hdpa);
    for (int i = 0; i < count; i++)
{
    delete [] (LPWSTR)DPA_GetPtr(_hdpa, i);
}
}  
```

下面的代码示例可避免此警告：

```
void Func()
{
    WCHAR*pszBuf=newWCHAR[MAX_PATH];
    if (DPA_ERR == DPA_InsertPtr(_hdpa, DA_LAST, pszBuf))
    {
        delete [] pszBuf;
    }

}

void CleanupDPA()
{
    int count = DPA_GetCount(_hdpa);
    for (int i = 0; i < count; i++)
{
    delete [] (LPWSTR)DPA_GetPtr(_hdpa, i);
}
}  
```









