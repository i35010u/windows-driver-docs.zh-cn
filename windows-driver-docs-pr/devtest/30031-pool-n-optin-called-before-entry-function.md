---
title: C30031
description: 警告 C30031 调用内存分配函数并传递一个参数，指示可执行文件的内存。
ms.assetid: 5DBC7AC3-30CA-4BD4-BBCB-2275033FF505
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C30031
ms.openlocfilehash: 74761caf9fcb7c192aaaf582410a198955e08e25
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371469"
---
# <a name="c30031"></a>C30031


警告 C30031:调用内存分配函数并传递一个参数，指示可执行文件的内存

代码分析检测到使用[池\_NX\_OPTIN](https://docs.microsoft.com/windows-hardware/drivers/kernel/single-binary-opt-in-pool-nx-optin)并**ExInitializeDriverRuntime (*DrvRtPoolNxOptIn*)** 之前调用入口函数 (例如， **DriverEntry()** 或**DllInitialize()** )。 可能的入口函数间接调用**ExInitializeDriverRuntime (*DrvRtPoolNxOptIn*)** ，可在这种情况下禁止错误 (请参阅[到禁止的杂注 Prefast警告消息](https://docs.microsoft.com/previous-versions/windows/embedded/gg155764(v=winembedded.70)))。

已禁止\_内存优化\_分配\_也许\_安全

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>示例


下面的代码的源文件中生成此警告：

```
C_DEFINES=$(C_DEFINES) -DPOOL_NX_OPTIN=1
```

在代码文件

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

 

 





