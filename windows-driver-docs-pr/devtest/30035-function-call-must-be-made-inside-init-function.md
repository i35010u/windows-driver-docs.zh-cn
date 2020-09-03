---
title: C30035
description: '警告 C30035 调用了一个函数，该函数必须在初始化函数内进行 (例如，DriverEntry ( # A2 或 DllInitialize ( # A4 # A5。 PREfast 无法确定是否从初始化函数进行调用。'
ms.assetid: 1A5F97EA-7DDC-4D3A-8058-B9C0C2211DA9
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C30035
ms.openlocfilehash: 62846fc5398fdf5d2b97f9a5ff658aee3adc5846
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384579"
---
# <a name="c30035"></a>C30035


警告 C30035：调用了一个函数，该函数必须在初始化函数内进行 (例如， **DriverEntry ( # B2 ** 或 **DllInitialize ( # B4 **) 。 PREfast 无法确定是否从初始化函数进行调用。

禁止的 \_ 内存 \_ 分配可能是错误的 \_ \_ \_ 调用 \_ 站点

此代码是用 [POOL \_ NX \_ OPTIN](../kernel/single-binary-opt-in-pool-nx-optin.md) 宏编译的，但初始化未在 **DriverEntry ( # B1 ** 或 **DllInitialize ( # B3 **内发生。 若要解决此问题，请将调用移到初始化函数内。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>实例


下面的代码将生成此警告。

在源文件中：

```
C_DEFINES=$(C_DEFINES) -DPOOL_NX_OPTIN=1
```

```
NTSTATUS
DriverEntry (
    _In_ PDRIVER_OBJECT DriverObject,
    _In_ PUNICODE_STRING RegistryPath
    )
{
    NTSTATUS status;

    MakeSafeInitialization ();
…
}

void MakeSafeInitialization()
{
    ExInitializeDriverRuntime(DrvRtPoolNxOptIn);
}
```

下面的代码可避免此警告：

```
NTSTATUS
DriverEntry (
    _In_ PDRIVER_OBJECT DriverObject,
    _In_ PUNICODE_STRING RegistryPath
    )
{
    NTSTATUS status;

    ExInitializeDriverRuntime(DrvRtPoolNxOptIn);
…
}
```

 

