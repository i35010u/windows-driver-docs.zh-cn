---
title: C30033
description: 警告在使用 POOL_NX_OPTIN 编译的驱动程序中检测到 C30033 可执行文件分配。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C30033
ms.openlocfilehash: 01c711f0dfab01579ce05c5ab4e0b9d11fb96548
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818609"
---
# <a name="c30033"></a>C30033


警告 C30033：在使用 [池 \_ NX \_ OPTIN](../kernel/single-binary-opt-in-pool-nx-optin.md)编译的驱动程序中检测到可执行的分配。 已确定此驱动程序在运行时由另一个驱动程序加载。 请验证加载驱动程序是否在其 DriverEntry 中调用了 **ExInitializeDriverRuntime (*DrvRtPoolNxOptIn*)** 。

禁止的 \_ 内存 \_ 分配可能会 \_ \_ 加载不安全的 \_ 驱动程序 \_

已确定这是由另一个驱动程序加载的 DLL，因此没有完整的初始化函数。 验证加载驱动程序是否为：

-   使用 [POOL \_ NX \_ OPTIN](../kernel/single-binary-opt-in-pool-nx-optin.md)= 1 编译
-   在其初始化函数中调用 **ExInitializeDriverRuntime (*DrvRtPoolNxOptIn*)**

如果加载驱动程序指定了这些正确的，则可以忽略此警告。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>实例


DLL 的每个加载器中的以下代码都意味着应按照以下安全示例 (进行更改) 

在源文件中

```
C_DEFINES=$(C_DEFINES)
```

在 **DriverEntry** 中，在发生任何内存分配之前：

```
NTSTATUS
DriverEntry (
    _In_ PDRIVER_OBJECT DriverObject,
    _In_ PUNICODE_STRING RegistryPath
    )
{
    NTSTATUS status;
…
    // No call to ExInitializeDriverRuntime
    return(status)
}
```

DLL 的每个加载器中的以下代码都意味着可以忽略此警告。

在源文件中，添加

```
C_DEFINES=$(C_DEFINES) -DPOOL_NX_OPTIN=1
```

在 **DriverEntry** 中，在发生任何内存分配之前：

```
NTSTATUS
DriverEntry (
    _In_ PDRIVER_OBJECT DriverObject,
    _In_ PUNICODE_STRING RegistryPath
    )
{
    NTSTATUS status;

    ExInitializeDriverRuntime( DrvRtPoolNxOptIn );
…
```

## <a name="span-idexample2spanspan-idexample2spanspan-idexample2spanexample-2"></a><span id="Example2"></span><span id="example2"></span><span id="EXAMPLE2"></span>示例 #2


解决此问题的另一种方法是使每个调用都显式引用不可执行的内存。

下面的代码将生成此警告。

```
ExAllocatePoolWithTag(NonPagedPool, numberOfBytes, 'xppn');
```

下面的代码可避免此警告：

```
ExAllocatePoolWithTag(NonPagedPoolNx, numberOfBytes, 'xppn');
```

 

