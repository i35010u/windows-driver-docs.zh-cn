---
title: 内核同步延迟模糊处理
description: 内核同步延迟模糊化选项随机化线程计划，以帮助检测驱动程序中的并发 bug。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5915ed3849ba6b5f0531a995611690c32ba77033
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806473"
---
# <a name="kernel-synchronization-delay-fuzzing"></a>内核同步延迟模糊处理

>[!Note]
> **从 Windows 10 预览体验版本19042及更高版本开始，此检查已弃用**

内核同步延迟模糊化选项随机化线程计划，以帮助检测驱动程序中的并发 bug。

**警告**  当验证计算机上的所有 (或大量) 驱动程序时，不应使用此选项。 仅当对单独驱动程序或其附加的筛选器驱动程序进行目标测试时，才应使用此选项。 同时对大量驱动程序使用此选项可能会导致不可预知的结果，并会在与你测试)  (的驱动程序无关的组件中强制崩溃。

 

**注意**  此选项可从 Windows 8.1 开始使用。

 

选择该选项时，驱动程序验证器会在线程中的不同时间点插入随机延迟。 与 [Power Framework 延迟模糊化](concurrency-stress-test.md) 选项类似，内核同步延迟模糊化选项使用一种算法，该算法可帮助提高在驱动程序中查找错误的几率。 内核同步延迟模糊处理在传统的压力测试上得以改进，其中，测试程序将在几天甚至几周内运行，以便能够在并发执行中出现问题。

## <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项


您可以使用驱动程序验证器管理器或 Verifier.exe 命令行为一个或多个驱动程序激活内核同步延迟模糊处理功能。 有关详细信息，请参阅 [选择驱动程序验证程序选项](selecting-driver-verifier-options.md)。 您必须重新启动计算机以激活或停用 Power Framework 延迟模糊化选项。

**注意**  内核同步延迟模糊化选项通过在各种内核 API 函数调用中插入随机延迟，增加了运行时出现的争用条件的概率。 为了使这些延迟更为有效，可以使用其他驱动程序验证程序选项启用此选项。 由于可能会引入延迟，因此可能会预计计算机响应速度较慢。

 

-   **在命令行中**

    在命令行中，内核同步延迟模糊处理由 **verifier/flags 0x00800000** (位 23) 表示。 若要激活 Power Framework 延迟模糊功能，请使用0x00800000 的标志值或将0x00800000 添加到标志值。 例如：

    ```
    verifier /flags 0x00800000 /driver MyDriver.sys
    ```

    此功能将在下一次启动后处于活动状态。

-   **使用驱动程序验证器管理器**

    1.  启动驱动程序验证器管理器。 在命令提示符窗口中键入 **Verifier** 。
    2.  选择 " **为代码开发人员 (创建自定义设置")** ，然后单击 " **下一步**"。
    3.  选择 " **从完整列表中选择单个设置**"。
    4.  选择 (检查) **内核同步延迟模糊** 处理。
    5.  重新启动计算机。

## <a name="span-idwhy_kernel_synchronization_delay_fuzzing_spanspan-idwhy_kernel_synchronization_delay_fuzzing_spanspan-idwhy_kernel_synchronization_delay_fuzzing_spanwhy-kernel-synchronization-delay-fuzzing"></a><span id="Why_Kernel_synchronization_delay_fuzzing_"></span><span id="why_kernel_synchronization_delay_fuzzing_"></span><span id="WHY_KERNEL_SYNCHRONIZATION_DELAY_FUZZING_"></span>为什么内核同步延迟模糊处理？


大多数驱动程序例程是可重入和并发的。 难以找到与并发相关的 bug。 Bug 可能包括死锁和争用条件，这是由同步问题和线程之间的错误计时导致的。 压力测试是用于查找这些 bug 的传统测试方法，但这种方法可能比较慢且成本高昂，并且结果并不总是可重现。 内核同步延迟模糊化选项通过在各种内核 API 函数调用中插入随机延迟，增加了运行时出现的争用条件的概率。 例如，如果争用条件导致驱动程序在取消后访问 IRP，则内核同步延迟模糊化选项将增加此争用条件的可能性，从而导致驱动程序验证器在测试过程中检测到错误。 内核同步延迟模糊化选项增强了驱动程序验证程序的功能和有效性。

 

 





