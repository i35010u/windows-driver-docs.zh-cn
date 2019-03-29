---
title: 在 WDM 驱动程序中使用浮点数
description: 使用浮点运算时，Windows 内核模式 WDM 驱动程序必须遵循特定的准则。 X86 和 x64 的系统之间存在差异。 默认情况下，Windows 将关闭这两个系统的算术异常。
ms.assetid: 73414084-4054-466a-b64c-5c81b224be92
keywords:
- 浮动点 WDK 内核
- 浮点单元 WDK 内核
- FPU WDK 内核
- KeSaveFloatingPointState
- KeRestoreFloatingPointState
- WDM 驱动程序 WDK 内核，浮点运算
- MMX WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a6235167e1d91c94fa3d9c60f6f1dc50eb3d4a9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575148"
---
# <a name="using-floating-point-in-a-wdm-driver"></a>在 WDM 驱动程序中使用浮点数


**上次更新时间**

-   2016 年 7 月

使用浮点运算时，Windows 内核模式 WDM 驱动程序必须遵循特定的准则。 X86 和 x64 的系统之间存在差异。 默认情况下，Windows 将关闭这两个系统的算术异常。

## <a name="x86-systems"></a>x86 系统


针对 x86 系统必须包装的浮动点计算调用之间使用的内核模式 WDM 驱动程序[ **KeSaveExtendedProcessorState** ](https://msdn.microsoft.com/library/windows/hardware/ff553238)并[ **KeRestoreExtendedProcessorState**](https://msdn.microsoft.com/library/windows/hardware/ff553182)。 浮点运算必须放置在非内联子例程，以确保不会检查的返回值之前执行浮点计算**KeSaveExtendedProcessorState**由于编译器重新排序。

编译器进行的 MMX/x87 浮点单元 (FPU) 也称为注册用于此类计算，在用户模式应用程序可以同时使用。 无法保存这些寄存器，然后才能使用它们，或失败来还原它们完成后，可能在应用程序中导致计算错误。

驱动程序针对 x86 系统可以调用[ **KeSaveExtendedProcessorState** ](https://msdn.microsoft.com/library/windows/hardware/ff553238) ，并执行浮点计算在 IRQL &lt;= 调度\_级别。 浮点运算不支持在 x86 上的中断服务例程 (Isr) 系统。

## <a name="x64-systems"></a>x64 系统


64 位编译器不使用 MMX/x87 寄存器浮点运算。 相反，它使用 SSE 寄存器。 x64 内核模式代码不允许访问 MMX/x87 寄存器。 编译器还负责正确保存和还原 SSE 状态，因此，调用[ **KeSaveExtendedProcessorState** ](https://msdn.microsoft.com/library/windows/hardware/ff553238)并[ **KeRestoreExtendedProcessorState** ](https://msdn.microsoft.com/library/windows/hardware/ff553182)是不必要和浮动点可在 Isr 操作。 AVX 等其他扩展的处理器功能的使用、 需要保存和还原扩展的状态。 有关详细信息请参阅[使用扩展 Windows 驱动程序中的处理器功能](floating-point-support-for-64-bit-drivers.md)。

## <a name="example"></a>示例


下面的示例演示如何 WDM 驱动程序应换行的 FPU 访问权限：

```cpp
__declspec(noinline)
VOID
DoFloatingPointCalculation(
    VOID
    )
{
    double Duration;
    LARGE_INTEGER Frequency;

    Duration = 1000000.0;
    DbgPrint("%I64x\n", *(LONGLONG*)&Duration);
    KeQueryPerformanceCounter(&Frequency);
    Duration /= (double)Frequency.QuadPart;
    DbgPrint("%I64x\n", *(LONGLONG*)&Duration);
}

NTSTATUS
DriverEntry(
    _In_ PDRIVER_OBJECT DriverObject,
    _In_ PUNICODE_STRING RegistryPath
    )
{

    XSTATE_SAVE SaveState;
    NTSTATUS Status;

    Status = KeSaveExtendedProcessorState(XSTATE_MASK_LEGACY, &SaveState);
    if (!NT_SUCCESS(Status)) {
        goto exit;
    }

    __try {
        DoFloatingPointCalculation();
    }
    __finally {
        KeRestoreExtendedProcessorState(&SaveState);
    }

exit:
    return Status;
}
```

在示例中，则浮点变量的赋值发生调用之间[ **KeSaveExtendedProcessorState** ](https://msdn.microsoft.com/library/windows/hardware/ff553238)并[ **KeRestoreExtendedProcessorState**](https://msdn.microsoft.com/library/windows/hardware/ff553182). 由于任何分配给浮点变量使用 FPU，驱动程序必须确保**KeSaveExtendedProcessorState**已返回而不返回错误之前初始化此类变量。

前面的调用是不必要在 x64 系统和无害时 XSTATE\_掩码\_指定旧标志。 因此，没有必要更改的代码在编译 x64 的驱动程序时系统。

在基于 x86 的系统，FPU 重置为其默认状态通过 FNINIT，从返回时调用[ **KeSaveExtendedProcessorState**](https://msdn.microsoft.com/library/windows/hardware/ff553238)。

 

 




