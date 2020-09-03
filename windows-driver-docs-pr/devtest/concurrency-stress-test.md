---
title: 电源框架延迟模糊处理
description: Power Framework 延迟模糊化选项随机化线程计划，以帮助检测使用电源管理框架 (PoFx) 的驱动程序中的并发 bug。
ms.assetid: A33DEA5B-4758-456A-B4CF-F036CB511A1F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bd2dde0b58b852313f616bdbbdc0a13bf1adc9e
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383693"
---
# <a name="power-framework-delay-fuzzing"></a>电源框架延迟模糊处理


Power Framework 延迟模糊化选项随机化线程计划，以帮助检测使用 [电源管理框架 (PoFx) ](../kernel/overview-of-the-power-management-framework.md)的驱动程序中的并发 bug。 对于不直接利用电源管理框架 (PoFx) 的驱动程序，不建议使用此选项。

**注意**   从 Windows 8 开始可以使用此选项。

 

选择该选项时，驱动程序验证器会在线程中的不同时间点插入随机延迟。 Power Framework 延迟模糊化选项使用一种算法，该算法可提供概率保证来查找驱动程序中的错误。 Power Framework 延迟模糊功能改进了传统的压力测试，其中的测试程序运行了几天甚至几周的时间，可以在并发执行中出现问题。

大多数驱动程序例程是可重入和并发的。 很难找到并发 bug。 Bug 可能包括死锁和争用条件，这是由同步问题和线程之间的错误计时导致的。 压力测试是一种传统的测试技术，但它可能会很慢且成本高昂，并且结果并不总是重复的。 Power Framework 延迟模糊化选项通过在各种 Power API 函数调用中插入随机延迟，增加了运行时出现的争用条件的概率。 例如，如果某个争用条件导致驱动程序在其取消后访问 IRP，则 Power Framework 延迟模糊化选项将增加此争用条件的可能性，从而导致驱动程序验证器在测试过程中检测到错误。 Power Framework 延迟模糊化选项扩展了驱动程序验证程序的功能和有用性。

## <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项


您可以使用驱动程序验证器管理器或 Verifier.exe 命令行为一个或多个驱动程序激活 Power Framework 延迟模糊功能。 有关详细信息，请参阅 [选择驱动程序验证程序选项](selecting-driver-verifier-options.md)。 您必须重新启动计算机以激活或停用 Power Framework 延迟模糊化选项。

**注意**   Power Framework 延迟模糊化选项通过在各种 Power API 函数调用中插入随机延迟，增加了运行时出现的争用条件的概率。 为了使这些延迟更为有效，可以使用其他驱动程序验证程序选项启用此选项。 由于可能会引入延迟，因此可能会预计计算机响应速度较慢。

 

-   **在命令行中**

    在命令行中，Power Framework 延迟模糊由 **verifier/flags 0x00008000 (位 15) **表示。 若要激活 Power Framework 延迟模糊功能，请使用0x00008000 的标志值或将0x00008000 添加到标志值。 例如：

    ```
    verifier /flags 0x00008000 /driver MyDriver.sys
    ```

    此功能将在下一次启动后处于活动状态。

-   **使用驱动程序验证器管理器**

    1.  启动驱动程序验证器管理器。 在命令提示符窗口中键入 **Verifier** 。
    2.  选择 " **为代码开发人员 (创建自定义设置") ** ，然后单击 " **下一步**"。
    3.  选择 " **从完整列表中选择单个设置**"。
    4.  选择 (检查) Power Framework 延迟模糊。
    5.  重新启动计算机。

 

