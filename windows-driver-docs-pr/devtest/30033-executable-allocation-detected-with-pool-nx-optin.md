---
title: C30033
description: 检测警告 C30033 可执行文件分配到使用 POOL_NX_OPTIN 编译到驱动程序。
ms.assetid: A5212960-F33D-485A-9B80-23F3D95D475C
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C30033
ms.openlocfilehash: a13b4cfc8476655fa240e415e4c2d20d2e27c0f4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562643"
---
# <a name="c30033"></a>C30033


警告 C30033:使用编译的驱动程序中，检测到可执行文件的分配[池\_NX\_OPTIN](https://msdn.microsoft.com/library/windows/hardware/hh920402)。 此驱动程序已确定要在加载运行时由另一个驱动程序。 请验证是否加载驱动程序调用**ExInitializeDriverRuntime (*DrvRtPoolNxOptIn*)** 其 DriverEntry 中。

已禁止\_内存优化\_分配\_也许\_UNSAFE\_驱动程序\_LOADED

已确定这是由另一个驱动程序，加载并没有这种情况下完成初始化函数的 DLL。 验证加载驱动程序：

-   使用编译[池\_NX\_OPTIN](https://msdn.microsoft.com/library/windows/hardware/hh920402)= 1
-   Calls **ExInitializeDriverRuntime(*DrvRtPoolNxOptIn*)** in its initialization function

如果加载驱动程序正确指定这些，可以忽略此警告。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>示例


每个加载的 DLL 的程序中的以下代码意味着您应更改 （根据安全下面的示例）

源文件中

```
C_DEFINES=$(C_DEFINES)
```

在中**DriverEntry**、 任何内存分配发生之前：

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

每个加载的 DLL 的程序中的以下代码意味着你可以忽略该警告。

在源文件中，添加

```
C_DEFINES=$(C_DEFINES) -DPOOL_NX_OPTIN=1
```

在中**DriverEntry**、 任何内存分配发生之前：

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

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>示例


若要解决此问题的第二种方法是使显式引用非可执行文件的内存的每个调用。

下面的代码生成此警告。

```
ExAllocatePoolWithTag(NonPagedPool, numberOfBytes, 'xppn');
```

下面的代码可避免此警告：

```
ExAllocatePoolWithTag(NonPagedPoolNx, numberOfBytes, 'xppn');
```

 

 





