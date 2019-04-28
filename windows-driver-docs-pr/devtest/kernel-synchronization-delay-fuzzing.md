---
title: 内核同步延迟模糊处理
description: 内核同步延迟模糊化选项随机排列线程计划来帮助检测驱动程序中的并发 bug。
ms.assetid: B4BB3A75-C458-4718-8BE9-065CFC09E194
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bbbc061191211991fd68db65e2fa4f5da301109
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340453"
---
# <a name="kernel-synchronization-delay-fuzzing"></a>内核同步延迟模糊处理


内核同步延迟模糊化选项随机排列线程计划来帮助检测驱动程序中的并发 bug。

**谨慎**  此选项不适用于使用当你要验证所有 （或大量的集合） 的计算机上的驱动程序。 仅当你正在单个驱动程序或其附加的筛选器驱动程序的目标测试时，应使用此选项。 在同一时间使用大量的驱动程序在此选项可能会导致不可预知的结果，并可以强制与正在测试驱动程序无关的组件中发生故障。

 

**请注意**  此选项是从 Windows 8.1 开始提供。

 

选中该选项后，驱动程序验证程序将在线程中的不同位置插入随机延迟。 像[电源框架延迟模糊](concurrency-stress-test.md)选项，内核同步延迟模糊化选项使用一种算法，提供了帮助提高驱动程序中查找错误的可能性。 内核同步延迟模糊改进了传统的压力测试，其中测试程序运行时的几天甚至几周以确保其达到捕获在发生的问题，可以在并发执行。

## <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项


您可以激活模糊化使用驱动程序验证程序管理器或 Verifier.exe 命令行的一个或多个驱动程序的功能的内核同步延迟。 有关详细信息，请参阅[选择 Driver Verifier 选项](selecting-driver-verifier-options.md)。 必须重新启动计算机以激活或停用电源框架延迟模糊选项。

**请注意**  模糊化选项内核同步延迟会延长的争用条件，使其不显示在运行时通过在不同的内核 API 函数调用中插入随机的延迟的概率。 对于更具效益这些延迟，可以启用此选项与其他驱动程序验证程序选项。 由于可以引入的延迟问题，您可以预计计算机具有响应越慢。

 

-   **在命令行**

    在命令行中，在由表示内核同步延迟模糊**verifier /flags 0x00800000** (位 23)。 若要激活电源框架延迟模糊，使用 0x00800000 标志值，或将 0x00800000 添加到标志值。 例如：

    ```
    verifier /flags 0x00800000 /driver MyDriver.sys
    ```

    在下一次启动后，该功能将处于活动状态。

-   **使用驱动程序验证程序管理器**

    1.  启动驱动程序验证器管理器。 类型**Verifier**在命令提示符窗口中。
    2.  选择**创建自定义设置 （适用于代码开发人员）** ，然后单击**下一步**。
    3.  选择**从完整的列表中选择单个设置**。
    4.  选择 （选中）**内核同步延迟模糊**。
    5.  重新启动计算机。

## <a name="span-idwhykernelsynchronizationdelayfuzzingspanspan-idwhykernelsynchronizationdelayfuzzingspanspan-idwhykernelsynchronizationdelayfuzzingspanwhy-kernel-synchronization-delay-fuzzing"></a><span id="Why_Kernel_synchronization_delay_fuzzing_"></span><span id="why_kernel_synchronization_delay_fuzzing_"></span><span id="WHY_KERNEL_SYNCHRONIZATION_DELAY_FUZZING_"></span>为什么内核同步延迟模糊？


大多数驱动程序例程是可重入和并发。 与相关的并发 bug 很难找到。 Bug 可以包括死锁和争用条件、 同步问题和错误计时之间的线程导致的。 压力测试是传统的测试技术用于查找这些 bug，但它可以慢速且昂贵的并且结果并不总是可重现。 内核同步延迟模糊化选项提高争用条件，使其不显示在运行时通过在不同的内核 API 函数调用中插入随机的延迟的可能性。 例如，如果争用条件导致驱动程序已取消后访问 IRP，模糊化选项内核同步延迟会延长此争用条件驱动程序验证程序在测试期间检测到将该错误的方式的可能性。 内核同步延迟模糊化选项增强了的强大功能和驱动程序验证程序的效率。

 

 





