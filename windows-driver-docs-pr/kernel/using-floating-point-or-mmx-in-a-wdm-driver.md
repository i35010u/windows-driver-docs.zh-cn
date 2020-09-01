---
title: 在 WDM 驱动程序中使用浮点数
description: 使用浮点运算时，适用于 Windows 的内核模式 WDM 驱动程序必须遵循特定的准则。 它们在 x86 和 x64 系统之间存在差异。 默认情况下，Windows 会关闭这两个系统的算术异常。
ms.assetid: 73414084-4054-466a-b64c-5c81b224be92
keywords:
- 浮点 WDK 内核
- 浮点单元
- FPU WDK 内核
- KeSaveFloatingPointState
- KeRestoreFloatingPointState
- WDM 驱动程序 WDK 内核，浮点运算
- MMX WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a9d56adc937b17fe1cceac2d6aa3fcc8a4d1941
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184973"
---
# <a name="using-floating-point-in-a-wdm-driver"></a>在 WDM 驱动程序中使用浮点数


**上次更新时间**

-   2016 年 7 月

使用浮点运算时，适用于 Windows 的内核模式 WDM 驱动程序必须遵循特定的准则。 它们在 x86 和 x64 系统之间存在差异。 默认情况下，Windows 会关闭这两个系统的算术异常。

## <a name="x86-systems"></a>x86 系统


X86 系统的内核模式 WDM 驱动程序必须在对 [**KeSaveExtendedProcessorState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesaveextendedprocessorstate) 和 [**KeRestoreExtendedProcessorState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kerestoreextendedprocessorstate)的调用之间换行使用浮点计算。 必须将浮点运算置于非内联子例程，以确保在检查 **KeSaveExtendedProcessorState** 的返回值之前不会执行浮点计算，因为编译器重新排序。

编译器利用 MMX/x87 （也称为浮点单元） (FPU) 注册此类计算，用户模式应用程序可以同时使用这些计算。 如果在使用这些寄存器之前未将其保存，或者无法在完成时将其还原，则可能会导致应用程序中出现计算错误。

X86 系统的驱动程序可以调用 [**KeSaveExtendedProcessorState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesaveextendedprocessorstate) ，并以 IRQL &lt; = 调度级别执行浮点计算 \_ 。  (x86 系统上的 Isr) 的中断服务例程不支持浮点运算。

## <a name="x64-systems"></a>x64 系统


64位编译器不将 MMX/x87 寄存器用于浮点运算。 相反，它使用 SSE 寄存器。 不允许 x64 内核模式代码访问 MMX/x87 寄存器。 编译器还会负责正确保存和还原 SSE 状态，因此，对 [**KeSaveExtendedProcessorState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesaveextendedprocessorstate) 和 [**KeRestoreExtendedProcessorState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kerestoreextendedprocessorstate) 的调用是不必要的，并且可以在 isr 中使用浮点运算。 使用其他扩展处理器功能（如 AVX）需要保存和还原扩展状态。 有关详细信息，请参阅 [在 Windows 驱动程序中使用扩展处理器功能](floating-point-support-for-64-bit-drivers.md)。

## <a name="example"></a>示例


下面的示例演示了 WDM 驱动程序应如何包装其 FPU 访问：

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

在此示例中，对 [**KeSaveExtendedProcessorState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesaveextendedprocessorstate) 和 [**KeRestoreExtendedProcessorState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kerestoreextendedprocessorstate)的调用之间发生浮点变量的赋值。 由于对浮点变量的任何赋值都使用了 FPU，因此，驱动程序必须确保 **KeSaveExtendedProcessorState** 在初始化此类变量之前已返回且没有错误。

在 x64 系统上无需进行上述调用，当 \_ 指定 XSTATE 掩码旧标志时，就不会造成危害 \_ 。 因此，编译 x64 系统的驱动程序时，无需更改代码。

在基于 x86 的系统上，从 [**KeSaveExtendedProcessorState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesaveextendedprocessorstate)返回后，FPU 会通过对 FNINIT 的调用重置为其默认状态。

 

