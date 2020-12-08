---
title: C28644
description: 警告 C28644 返回值未选中 DPA_InsertPtr。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28644
ms.openlocfilehash: 32dbaeb6d5f7d6b7b44f5ad8a51e3904061aa90b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840197"
---
# <a name="c28644"></a>C28644


警告 C28644：未检查 DPA InsertPtr 的返回值 \_

此警告表明内存可能泄漏。

大多数对 [**DPA \_ InsertPtr**](/windows/win32/api/dpa_dsa/nf-dpa_dsa-dpa_insertptr) 函数的调用都使用在堆上分配的变量。 然后，函数使用 DPA，并释放 DPA 中存储的所有对象。 当 **dpa \_ InsertPtr** 失败时，将无法再通过 dpa 清理代码释放已分配的对象，因此 **dpa \_ InsertPtr** 的调用方需要释放内存。 请注意，在以下示例中调用了 **CleanupDPA** 。 如果代码未以类似于 **CleanupDPA** 的方式释放已分配的对象，则可能无需修复任何问题。 此缺陷假设我们依赖于 DPA 来跟踪我们在以后可用的所有对象。

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
