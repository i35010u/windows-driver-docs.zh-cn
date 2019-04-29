---
title: 使用 Windows 驱动程序中扩展的处理器功能
description: 使用扩展的处理器功能的 x86 和 x64 系统的 Windows 驱动程序必须包装对和调用之间 KeSaveExtendedProcessorState KeRestoreExtendedProcessorState 以避免在并发应用程序中的错误浮点计算的可能会使用寄存器。
ms.assetid: a42e86cf-47a2-44ed-8bf1-7407633af8b7
keywords:
- 浮动点 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1f893e4917e3bb82e091ae372b017f7cf11f14f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359950"
---
# <a name="using-extended-processor-features-in-windows-drivers"></a>使用 Windows 驱动程序中扩展的处理器功能


**上次更新时间**

-   2016 年 7 月

使用扩展的处理器功能的 x86 和 x64 系统的 Windows 驱动程序必须包装浮点计算调用之间[ **KeSaveExtendedProcessorState** ](https://msdn.microsoft.com/library/windows/hardware/ff553238)和[ **KeRestoreExtendedProcessorState** ](https://msdn.microsoft.com/library/windows/hardware/ff553182)以避免在并发应用程序可能使用寄存器中的错误。

## <a name="legacy-mmxx87-registers"></a>旧的 MMX x87 寄存器


这些寄存器对应于 XSTATE\_掩码\_旧版\_浮动\_点掩码和 x64 的驱动程序不可用的是系统。 有关详细信息，这些注册，请参阅[WDM 驱动程序中使用浮点](using-floating-point-or-mmx-in-a-wdm-driver.md)。

## <a name="sse-registers"></a>SSE 寄存器


这些寄存器对应于 XSTATE\_掩码\_旧版\_SSE 标志并由 x64 编译器的浮点运算。 驱动程序针对 x86 使用这些寄存器的系统必须将它们保存在使用之前通过传递 XSTATE\_掩码\_旧式或 XSTATE\_掩码\_旧版\_中的 SSE 标志[ **KeSaveExtendedProcessorState** ](https://msdn.microsoft.com/library/windows/hardware/ff553238)调用，并在完成后，将其与还原[ **KeRestoreExtendedProcessorState**](https://msdn.microsoft.com/library/windows/hardware/ff553182)。 这是在 x64 上不必要的系统，但没有坏处。 有关详细信息，有关这些注册，请参阅[WDM 驱动程序中使用浮点](using-floating-point-or-mmx-in-a-wdm-driver.md)。

## <a name="avx-registers"></a>AVX 寄存器


这些寄存器对应于 XSTATE\_掩码\_GSSE 或 XSTATE\_掩码\_AVX 掩码。 新的 x86 处理器，如 Intel 浅桥 (以前称为 Gesher) 处理器，支持 AVX 指令和集 (YMM0 YMM15) 注册。 在 Windows 7 Service Pack 1 (SP1)、 Windows Server 2008 R2，与较新版本的 Windows 中，x86 和 x64 版本的操作系统保留的 AVX 寄存器跨线程 （和进程） 开关。 若要在内核模式下使用 AVX 寄存器，驱动程序 （x86 和 x64） 必须显式保存和还原 AVX 寄存器。 不能使用 AVX 寄存器中中断服务例程，并默认关闭算术异常。

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
[**KeSaveExtendedProcessorState**](https://msdn.microsoft.com/library/windows/hardware/ff553238)  
[**KeRestoreExtendedProcessorState**](https://msdn.microsoft.com/library/windows/hardware/ff553182)  
[使用浮点 WDM 驱动程序中](using-floating-point-or-mmx-in-a-wdm-driver.md)  



