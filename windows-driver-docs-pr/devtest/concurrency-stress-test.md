---
title: 电源框架延迟模糊
description: 电源框架延迟模糊选项随机排列线程计划来帮助检测使用电源管理框架 (PoFx) 的驱动程序中的并发 bug。
ms.assetid: A33DEA5B-4758-456A-B4CF-F036CB511A1F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f3268173a4500e1111aa08ed4027f5190add8fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555669"
---
# <a name="power-framework-delay-fuzzing"></a>电源框架延迟模糊


电源框架延迟模糊选项随机排列线程计划，以帮助驱动程序中使用的检测并发 bug[电源管理框架 (PoFx)](https://msdn.microsoft.com/library/windows/hardware/hh406637)。 对不直接利用电源管理框架 (PoFx) 的驱动程序不建议使用此选项。

**请注意**  此选项才可用从 Windows 8 开始。

 

选中该选项后，驱动程序验证程序将在线程中的不同位置插入随机延迟。 电源框架延迟模糊选项使用一种算法，提供概率性保证驱动程序中查找错误。 电源框架延迟模糊改进了传统的压力测试，其中测试程序运行时的几天甚至几周以确保其达到捕获在发生的问题，可以在并发执行。

大多数驱动程序例程是可重入和并发。 并发 bug 很难找到。 Bug 可以包括死锁和争用条件、 同步问题和错误计时之间的线程导致的。 压力测试是传统的测试技术，但它可以慢速且昂贵的并且结果并不总是可重现。 电源框架延迟模糊选项会增加使其不显示在运行时通过在各种 power API 函数调用中插入随机的延迟的争用条件的概率。 例如，如果争用条件的结果后已取消访问 IRP 的驱动程序，电源框架延迟模糊选项会增加此争用条件驱动程序验证程序在测试期间检测到将该错误的方式的可能性。 电源框架延迟模糊选项扩展的强大功能和驱动程序验证程序的用途。

## <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项


可以使用驱动程序验证程序管理器或 Verifier.exe 命令行来激活一个或多个驱动程序的电源框架延迟模糊功能。 有关详细信息，请参阅[选择 Driver Verifier 选项](selecting-driver-verifier-options.md)。 必须重新启动计算机以激活或停用电源框架延迟模糊选项。

**请注意**  电源框架延迟模糊选项会增加使其不显示在运行时通过在各种 power API 函数调用中插入随机的延迟的争用条件的概率。 对于更具效益这些延迟，可以启用此选项与其他驱动程序验证程序选项。 由于可以引入的延迟问题，您可以预计计算机具有响应越慢。

 

-   **在命令行**

    在命令行中，在由表示电源框架延迟模糊**verifier /flags 0x00008000 (位 15)**。 若要激活电源框架延迟模糊，使用 0x00008000 标志值，或将 0x00008000 添加到标志值。 例如：

    ```
    verifier /flags 0x00008000 /driver MyDriver.sys
    ```

    在下一次启动后，该功能将处于活动状态。

-   **使用驱动程序验证程序管理器**

    1.  启动驱动程序验证器管理器。 类型**Verifier**在命令提示符窗口中。
    2.  选择**创建自定义设置 （适用于代码开发人员）** ，然后单击**下一步**。
    3.  选择**从完整的列表中选择单个设置**。
    4.  选择 （检查） 电源框架延迟模糊。
    5.  重新启动计算机。

 

 





