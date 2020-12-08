---
title: C28651
description: 警告 C28651 静态初始值设定项导致在写入页上复制，原因是成员函数指针。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28651
ms.openlocfilehash: 21e4af494deac36385bf9f0149dd797142134388
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794019"
---
# <a name="c28651"></a>C28651


警告 C28651：静态初始值设定项导致在写入页上复制，原因是成员函数指针

全局或静态 const 变量的静态初始值设定项通常可以在编译时完全计算，从而在 RDATA 中生成。 但是，如果任何初始值设定项是指向成员的指针函数（其中它是非静态函数），则整个初始值设定项可以置于 "写入时复制" 页中，这会产生性能开销。

对于需要快速加载和最小化写入页上副本的二进制文件，请考虑确保静态初始值设定项中的所有函数指针不是指向成员的指针函数。 如果需要指向成员的指针函数，请编写一个简单的静态成员函数，用于包装对实际成员函数的调用。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>实例


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









