---
title: C28651
description: 警告 C28651 静态初始值设定项导致由于成员函数指针的写入页上的副本。
ms.assetid: 2E7B61A7-FF15-46C3-87B4-36CAA2E52CAC
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28651
ms.openlocfilehash: 5b88a6b49e6bbfe43d99dd51563943688f3b92fe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555057"
---
# <a name="c28651"></a>C28651


警告 C28651:由于成员函数指针的写入页上的静态初始值设定项导致复制过程

静态初始值设定项的全局或静态的 const 变量可以通常是完全在编译时计算，因此 RDATA 中生成。 但如果任何初始值设定项是其所在的非静态函数指针到成员函数，整个初始值设定项可能会放置在写入时复制页面，其中具有性能成本。

对于需要快速加载和最大程度减少写入页上的复制的二进制文件，请考虑确保静态初始值设定项中的所有函数指针不都指针到成员函数。 如果指针到成员函数是必需的编写简单的静态成员函数包装对实际成员函数的调用。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>示例


下面的代码示例生成此错误。

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

下面的代码示例可避免此错误。

```
class MyClass
{
    ...
    bool memberFunc();
    static bool memberFuncWrap(MyClass *thisPtr)
        { return thisPtr->memberFunc(); }
    ...
};
const StructType MyStruct[] = {
    ...
    &MyClass::memberFuncWrap,
    ...
};  
```









