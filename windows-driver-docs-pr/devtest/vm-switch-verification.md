---
title: VM 交换机验证
description: VM 交换机验证选项可监视筛选器驱动程序 （可扩展交换机扩展），HYPER-V 可扩展交换机在中运行。 使用此选项以捕获错误发生在发送或接收可扩展交换机中的操作。
ms.assetid: 629C0C70-D6C6-4977-A36B-6BD6EEC14FE8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc4e109ef2cc85619259c4ff02f0c7073a45e4c7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381786"
---
# <a name="vm-switch-verification"></a>VM 交换机验证


VM 交换机验证选项可监视筛选器驱动程序 (*可扩展交换机扩展*) 内运行[HYPER-V 可扩展交换机](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch)。 使用此选项以捕获错误发生在发送或接收可扩展交换机中的操作。

**请注意**  此选项是从 Windows 8.1 开始提供。

 

驱动程序验证程序时此选项处于活动状态，将发出[ **Bug 检查 0xC4** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (驱动程序\_VERIFIER\_检测到\_冲突) 如果可扩展交换机扩展无法正确调用处理程序函数的 HYPER-V 可扩展交换机。

## <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项


可以使用驱动程序验证程序管理器或 Verifier.exe 命令行来激活一个或多个驱动程序的 VM 交换机验证功能。 有关详细信息，请参阅[选择 Driver Verifier 选项](selecting-driver-verifier-options.md)。 必须重新启动计算机以激活或停用电源框架延迟模糊选项。

-   **在命令行**

    在命令行中，VM 交换机验证为由**verifier /flags 0x01000000** (位 24)。 若要激活电源框架延迟模糊，使用标志值为 0x01000000，或将 0x01000000 添加到标志值。 例如：

    ```
    verifier /flags 0x01000000  /driver MyDriver.sys
    ```

    在下一次启动后，该功能将处于活动状态。

-   **使用驱动程序验证程序管理器**

    1.  启动驱动程序验证器管理器。 类型**Verifier**在命令提示符窗口中。
    2.  选择**创建自定义设置 （适用于代码开发人员）** ，然后单击**下一步**。
    3.  选择**从完整的列表中选择单个设置**。
    4.  选择 （选中） **VM 交换机验证**。
    5.  重新启动计算机。

 

 





