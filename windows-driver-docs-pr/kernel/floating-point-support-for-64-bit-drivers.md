---
title: 使用 Windows 驱动程序中扩展的处理器功能
description: 使用扩展处理器功能的 x86 和 x64 系统的 Windows 驱动程序必须在对 KeSaveExtendedProcessorState 和 KeRestoreExtendedProcessorState 的调用之间换行计算，以避免可能使用寄存器的并发应用程序中出现错误。
keywords:
- 浮点 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fb0d0412dc83fb303fedf09ff5a2520ca0b8880
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816639"
---
# <a name="using-extended-processor-features-in-windows-drivers"></a>使用 Windows 驱动程序中扩展的处理器功能


**上次更新时间**

-   2016 年 7 月

使用扩展处理器功能的 x86 和 x64 系统的 Windows 驱动程序必须在对 [**KeSaveExtendedProcessorState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesaveextendedprocessorstate) 和 [**KeRestoreExtendedProcessorState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kerestoreextendedprocessorstate) 的调用之间换行计算，以避免可能使用寄存器的并发应用程序中出现错误。

## <a name="legacy-mmxx87-registers"></a>旧 MMX/x87 寄存器


这些寄存器对应于 XSTATE \_ 掩码 \_ 旧版 \_ 浮点 \_ 掩码，适用于 x64 系统的驱动程序不可用。 有关这些寄存器的详细信息，请参阅 [在 WDM 驱动程序中使用浮点](using-floating-point-or-mmx-in-a-wdm-driver.md)。

## <a name="sse-registers"></a>SSE 注册


这些寄存器对应于 XSTATE \_ 掩码 \_ 旧版 \_ SSE 标志，并且由 x64 编译器用于浮点运算。 使用这些寄存器的 x86 系统的驱动程序必须在使用之前保存它们，方法 \_ 是 \_ 在 KeSaveExtendedProcessorState 调用中传递 XSTATE 掩码 LEGACY 或 XSTATE \_ 掩码 \_ 旧版 \_ SSE 标志，并在完成后使用 [**KeRestoreExtendedProcessorState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kerestoreextendedprocessorstate)还原它们。 [**KeSaveExtendedProcessorState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesaveextendedprocessorstate) 在 x64 系统上不需要这样做，但这不是有害的。 有关这些寄存器的详细信息，请参阅 [在 WDM 驱动程序中使用浮点](using-floating-point-or-mmx-in-a-wdm-driver.md)。

## <a name="avx-registers"></a>AVX 寄存器


这些寄存器对应于 XSTATE \_ mask \_ GSSE 或 XSTATE \_ mask AVX mask \_ 。 新的 x86 处理器，如 Intel Sandy Bridge (以前的 Gesher) 处理器，支持 AVX 说明， (YMM0-YMM15) 注册集。 在带有 Service Pack 1 的 Windows 7 (SP1) 、Windows Server 2008 R2 和更新版本的 Windows 中，x86 和 x64 版本的操作系统都将跨线程 (和处理) 开关来保持 AVX 寄存器。 若要使用内核模式下的 AVX 寄存器， (x86 和 x64) 的驱动程序必须显式保存并还原 AVX 寄存器。 AVX 寄存器不能用于中断服务例程，默认情况下，算术异常处于关闭状态。

```cpp
include ksamd64.inc

        subttl "Set YMM State."
;++
;
; Routine Description:
;   
;   This routine loads the first four YMM registers with the state supplied.
;
; Arguments;
;
;   rcx - Supplies a pointer to the values we want to load.
;
; Return Value:
;
;   None
;
;--

LEAF_ENTRY SetYmmValues, _TEXT$00

        vmovdqa    ymm0,  ymmword ptr[rcx + 0]
        vmovdqa    ymm1,  ymmword ptr[rcx + 32]
        vmovdqa    ymm2,  ymmword ptr[rcx + 64]
        vmovdqa    ymm3,  ymmword ptr[rcx + 96]

        ret

LEAF_END SetYmmValues, _TEXT$00

        end
```

```cpp
typedef DECLSPEC_ALIGN(32) struct _YMM_REGISTERS {
    ULONG64 Ymm4Registers[16];
} YMM_REGISTERS, *PYMM_REGISTERS;

VOID
FASTCALL
SetYmmValues(
    __in PYMM_REGISTERS YmmRegisterValues
    );

NTSTATUS
DriverEntry (
    __in PDRIVER_OBJECT DriverObject,
    __in PUNICODE_STRING RegistryPath
    )
{

    NTSTATUS Status;
    XSTATE_SAVE SaveState;
    ULONG64 EnabledFeatures;

    //
    // Load the first 4 YMM registers as 4 vectors of 4 64-bit integers.
    //

    YMM_REGISTERS RegisterValues = { 0, 1, 2, 3,        // YMM0
                                     4, 5, 6, 7,        // YMM1
                                     8, 9, 10, 11,      // YMM2
                                     12, 13, 14, 15 };  // YMM3

    //
    // Check to see if AVX is available. Bail if it is not.
    //

    EnabledFeatures = RtlGetEnabledExtendedFeatures(-1);
    if ((EnabledFeatures & XSTATE_MASK_GSSE) == 0) {
        Status = STATUS_FAILED_DRIVER_ENTRY;
        goto exit;
    }

    Status = KeSaveExtendedProcessorState(XSTATE_MASK_GSSE, &SaveState);

    if (!NT_SUCCESS(Status)) {
        goto exit;
    }

    __try {
        SetYmmValues(&RegisterValues);
    }
    __finally {
        KeRestoreExtendedProcessorState(&SaveState);
    }

exit:
    return Status;
}
```

## <a name="related-topics"></a>相关主题
[**KeSaveExtendedProcessorState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesaveextendedprocessorstate)  
[**KeRestoreExtendedProcessorState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kerestoreextendedprocessorstate)  
[在 WDM 驱动程序中使用浮点数](using-floating-point-or-mmx-in-a-wdm-driver.md)
