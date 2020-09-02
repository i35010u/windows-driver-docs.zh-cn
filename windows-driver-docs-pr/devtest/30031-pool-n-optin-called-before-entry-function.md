---
title: C30031
description: 警告 C30031 调用内存分配函数并传递指示可执行文件内存的参数。
ms.assetid: 5DBC7AC3-30CA-4BD4-BBCB-2275033FF505
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C30031
ms.openlocfilehash: 7c5e4c8c557027a13ce9ba94dbc7f21e4003ce73
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381641"
---
# <a name="c30031"></a>C30031


警告 C30031：调用内存分配函数并传递指示可执行内存的参数

代码分析检测到使用 [了 \_ 池 NX \_ OPTIN](../kernel/single-binary-opt-in-pool-nx-optin.md) 和 ExInitializeDriverRuntime (在 entry (函数之前调用 ** *DrvRtPoolNxOptIn*) ** 例如， **DriverEntry ( # B4 ** 或 **DllInitialize ( # B6 **) 。 入口函数可能会间接调用 **ExInitializeDriverRuntime (*DrvRtPoolNxOptIn*) **，在这种情况下，可以禁止显示错误 (请参阅 [杂注 Prefast 禁止显示) 的警告消息](/previous-versions/windows/embedded/gg155764(v=winembedded.70)) 。

禁止的 \_ 内存 \_ 分配可能是 \_ \_ 安全的

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>实例


源文件中的以下代码将生成此警告：

```
C_DEFINES=$(C_DEFINES) -DPOOL_NX_OPTIN=1
```

在代码文件中

```
void MakeSafeInitialization()
{
    ExInitializeDriverRuntime(DrvRtPoolNxOptIn);
}

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

 

