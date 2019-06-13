---
title: 为不同版本的 Windows 编写驱动程序
description: 为不同版本的 Windows 编写驱动程序
ms.assetid: 7519235c-46c5-49aa-8b11-9e9ac5a51026
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2e02f689d670af6d22b1d5b95f3d6775096ee87
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "63371203"
---
# <a name="writing-drivers-for-different-versions-of-windows"></a>为不同版本的 Windows 编写驱动程序


创建驱动程序项目时，请指定最低目标操作系统，该操作系统是运行驱动程序的 Windows 的最低版本。 例如，可以指定 Windows 7 为最低目标操作系统。 在这种情况下，驱动程序会在 Windows 7 和更高版本的 Windows 上运行。

**注意**  如果为特定的最低版本的 Windows 开发驱动程序且希望驱动程序运行在更高版本的 Windows 上，则不得使用任何未记录的函数，也不得以文档中介绍的方式之外的任何其他方式使用记录的函数。 否则，驱动程序可能会无法运行在更高版本的 Windows 上。 即使你已经很小心地仅使用记录的函数，也应在每次发布新版本的 Windows 时在其上对驱动程序进行测试。



## <a name="span-idwritingamultiversiondriverusingonlycommonfeaturesspanspan-idwritingamultiversiondriverusingonlycommonfeaturesspanspan-idwritingamultiversiondriverusingonlycommonfeaturesspanwriting-a-multiversion-driver-using-only-common-features"></a><span id="Writing_a_multiversion_driver_using_only_common_features"></span><span id="writing_a_multiversion_driver_using_only_common_features"></span><span id="WRITING_A_MULTIVERSION_DRIVER_USING_ONLY_COMMON_FEATURES"></span>编写仅使用共同功能的多版本驱动程序


设计将在多个版本的 Windows 上运行的驱动程序时，最简单的方法是允许驱动程序仅使用运行该驱动程序的所有版本的 Windows 共同的 DDI 函数和结构。 在此情形下，将最低目标操作系统设置为驱动程序将支持的最低 Windows 版本。

例如，若要支持从 Windows 7 开始的所有版本的 Windows，应执行以下操作：

1.  设计并实现驱动程序，以便该驱动程序仅使用 Windows 7 中提供的那些功能。

2.  生成驱动程序时，将 Windows 7 指定为最低目标操作系统。

虽然此过程很简单，但它可能会限制驱动程序仅使用更高版本的 Windows 上提供的功能子集。

## <a name="span-idwritingamultiversiondriverthatusesversion-dependentfeaturesspanspan-idwritingamultiversiondriverthatusesversion-dependentfeaturesspanspan-idwritingamultiversiondriverthatusesversion-dependentfeaturesspanwriting-a-multiversion-driver-that-uses-version-dependent-features"></a><span id="Writing_a_multiversion_driver_that_uses_version-dependent_features"></span><span id="writing_a_multiversion_driver_that_uses_version-dependent_features"></span><span id="WRITING_A_MULTIVERSION_DRIVER_THAT_USES_VERSION-DEPENDENT_FEATURES"></span>编写使用版本相关功能的多版本驱动程序


内核模式驱动程序可以动态确定它在哪个版本的 Windows 上运行并且选择使用该版本提供的功能。 例如，必须支持从 Windows 7 开始的所有 Windows 版本的驱动程序可以在运行时确定它在哪个 Windows 版本上运行。 如果驱动程序在 Windows 7 上运行，则它只能使用 Windows 7 支持的 DDI 函数。 但是，同一个驱动程序可以使用 Windows 8 独有的其他 DDI 函数，例如，当其运行时检查确定它在 Windows 8 上运行时。

### <a name="span-iddeterminingthewindowsversionspanspan-iddeterminingthewindowsversionspandetermining-the-windows-version"></a><span id="determining_the_windows_version"></span><span id="DETERMINING_THE_WINDOWS_VERSION"></span>确定 Windows 版本

[**RtlIsNtDdiVersionAvailable**](https://msdn.microsoft.com/library/windows/hardware/ff561954) 为驱动程序可以在运行时用于确定特定版本的 Windows 提供的功能是否可用的函数。 该函数的原型如下所示：

```cpp
BOOLEAN RtlIsNtDdiVersionAvailable(IN ULONG Version)
```

在此原型中，*Version* 是一个值，指示 Windows DDI 的所需版本。 此值必须为 sdkddkver.h 中定义的 DDI 版本常量之一，如 NTDDI\_WIN8 或 NTDDI\_WIN7。

当调用程序运行在与 *Version* 指定的相同的 Windows 版本上或比之更高的版本上时，[**RtlIsNtDdiVersionAvailable**](https://msdn.microsoft.com/library/windows/hardware/ff561954) 会返回 TRUE。

驱动程序还可以通过调用 [**RtlIsServicePackVersionInstalled**](https://msdn.microsoft.com/library/windows/hardware/ff561956) 函数来检查是否安装了特定的 Service Pack。 该函数的原型如下所示：

```cpp
BOOLEAN RtlIsServicePackVersionInstalled(IN ULONG Version)
```

在此原型中，*Version* 为一个值，指示所需的 Windows 版本和 Service Pack。 此值必须为 sdkddkver.h 中定义的 DDI 版本常量之一，如 NTDDI\_WS08SP3。

请注意，仅当操作系统版本与指定版本完全匹配时，[**RtlIsServicePackVersionInstalled**](https://msdn.microsoft.com/library/windows/hardware/ff561956) 才会返回 TRUE。 因此，如果驱动程序不是在 Windows Server 2008 SP4 上运行，则将 *Version* 设置为 NTDDI\_WS08SP3 的 **RtlIsServicePackVersionInstalled** 调用会失败。

### <a name="span-idconditionallycallingwindowsversiondependentfunctionsspanspan-idconditionallycallingwindowsversiondependentfunctionsspanconditionally-calling-windows-version-dependent-functions"></a><span id="conditionally_calling_windows_version_dependent_functions"></span><span id="CONDITIONALLY_CALLING_WINDOWS_VERSION_DEPENDENT_FUNCTIONS"></span>有条件地调用与 Windows 版本相关的函数

在驱动程序确定计算机上可用的特定操作系统版本后，该驱动程序可以使用 [**MmGetSystemRoutineAddress**](https://msdn.microsoft.com/library/windows/hardware/ff554563) 函数动态查找例程并通过指针调用该例程。 Windows 7 及更高操作系统版本上提供了此函数。

**注意**  若要帮助保留键入检查和防止出现无意识的错误，应创建映射原始函数类型的 typedef。



### <a name="span-idexampledeterminingthewindowsversionandconditionallycallingavspanspan-idexampledeterminingthewindowsversionandconditionallycallingavspanexample-determining-the-windows-version-and-conditionally-calling-a-version-dependent-function"></a><span id="example__determining_the_windows_version_and_conditionally_calling_a_v"></span><span id="EXAMPLE__DETERMINING_THE_WINDOWS_VERSION_AND_CONDITIONALLY_CALLING_A_V"></span>示例：确定 Windows 版本并有条件地调用与版本相关的函数

此代码示例（来自驱动程序的头文件）将 PAISQSL 类型定义为指向 [**KeAcquireInStackQueuedSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551899) 函数的指针。 然后，此示例声明该类型的 `AcquireInStackQueuedSpinLock` 变量。

```cpp
...
 //
// Pointer to the ordered spin lock function.
// This function is only available on Windows 7 and
// later systems
 typedef (* PAISQSL) (KeAcquireInStackQueuedSpinLock);
PAISQSL AcquireInStackQueued = NULL;
 ...
```

此代码示例（来自驱动程序的初始化代码）确定驱动程序是否在 Windows 7 或更高版本操作系统上运行。 如果是，代码会检索指向 [**KeAcquireInStackQueuedSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551899) 的指针。

```cpp
...

//
// Are we running on Windows 7 or later?
//
 if (RtlIsNtDdiVersionAvailable(NTDDI_WIN7) ) {

 //
  // Yes... Windows 7 or later it is!
  //
     RtlInitUnicodeString(&funcName,
                  L"KeAcquireInStackQueuedSpinLock");

 //
  // Get a pointer to Windows implementation
  // of KeAcquireInStackQueuedSpinLock into our
  // variable "AcquireInStackQueued"
     AcquireInStackQueued = (PAISQSL)
                  MmGetSystemRoutineAddress(&funcName);
 }

...
// Acquire a spin lock.

 if( NULL != AcquireInStackQueued) {
  (AcquireInStackQueued)(&SpinLock, &lockHandle);
} else {
    KeAcquireSpinLock(&SpinLock);
}
```

在此示例中，驱动程序调用 [**RtlIsNtDdiVersionAvailable**](https://msdn.microsoft.com/library/windows/hardware/ff561954) 以确定驱动程序是否在 Windows 7 或更高版本上运行。 如果版本为 Windows 7 或更高版本，驱动程序将会调用 [**MmGetSystemRoutineAddress**](https://msdn.microsoft.com/library/windows/hardware/ff554563) 来获取指向 [**KeAcquireInStackQueuedSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551899) 函数的指针并将此指针存储在名为 `AcquireInStackQueued` 的变量（该变量声明为 PAISQSL 类型）中。

随后，当驱动程序必须获取旋转锁时，它会检查是否收到了指向 [**KeAcquireInStackQueuedSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551899) 函数的指针。 如果驱动程序已收到此指针，则驱动程序会使用该指针调用 **KeAcquireInStackQueuedSpinLock**。 如果指向 **KeAcquireInStackQueuedSpinLock** 的指针为 Null，则驱动程序会使用 [**KeAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551917) 来获取旋转锁。









