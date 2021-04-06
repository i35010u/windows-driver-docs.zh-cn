---
title: 'UninitializedPtrField (补充 Windows 驱动程序 CodeQL 查询) '
description: UninitializedPtrField 补充 Windows Driver CodeQL 查询
ms.date: 01/11/2021
ms.localizationpriority: medium
ms.openlocfilehash: c239d9bdff1f53e8561bd7417cc11e815ef09bbc
ms.sourcegitcommit: 0e165d26ea3887d87eb41d591b8d847038a73085
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/05/2021
ms.locfileid: "106387618"
---
# <a name="uninitializedptrfield-windows-driver-codeql-query"></a>UninitializedPtrField (Windows Driver CodeQL Query) 

## <a name="overview"></a>概述

在或类构造过程中未初始化的指针字段将导致空指针取消引用。

## <a name="recommendation"></a>建议

请确保在使用之前初始化所有指针字段。

## <a name="example"></a>示例

下面的示例演示了一个方案，该方案中的字段 *ptr_* 不 initialzied，以后将取消引用：

```cpp
template <typename T>
class ComPtr
{
public:
    T* ptr_;
    ComPtr() throw() : ptr_(nullptr)
    {
    }
    ComPtr(T* ptr) throw() : ptr_(ptr)
    {
    }
    T* operator->() const throw()
    {
        return ptr_;
    }
    void set(T* ptr) {
        ptr_ = ptr;
    }
    T** addr() {
        return &ptr_;
    }
};

class Test
{
public:
    int it_;
    int it() {
        return it_;
    }
};
void test() {
    Test t;
    int val;
    ComPtr<Test> ptr;
    // BAD: pointer is not initialized here
    val = ptr->it();
}
```

若要解决此问题，我们在使用之前设置字段：

```cpp
template <typename T>
class ComPtr
{
public:
    T* ptr_;
    ComPtr() throw() : ptr_(nullptr)
    {
    }
    ComPtr(T* ptr) throw() : ptr_(ptr)
    {
    }
    T* operator->() const throw()
    {
        return ptr_;
    }
    void set(T* ptr) {
        ptr_ = ptr;
    }
    T** addr() {
        return &ptr_;
    }
};
class Test
{
public:
    int it_;
    int it() {
        return it_;
    }
};
void test() {
    Test t;
    int val;
    ComPtr<Test> ptr2(&t);
    // GOOD: pointer was initialized
    val = ptr2->it();
    ComPtr<Test> ptr3;
    ptr3.set(&t);
    // GOOD: pointer was set in between
    val = ptr3->it();
}
```

## <a name="additional-details"></a>其他详细信息

此查询可在 [Microsoft GitHub CodeQL 存储库](https://github.com/microsoft/Windows-Driver-Developer-Supplemental-Tools)中找到。  有关 Windows 驱动程序开发人员如何下载和运行 CodeQL 的详细信息，请参阅 [CodeQL 和静态工具徽标测试](./static-tools-and-codeql.md) 页。
