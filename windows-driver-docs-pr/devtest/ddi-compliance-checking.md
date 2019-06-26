---
title: DDI 合规性检查
description: DDI 符合性检查选项确定驱动程序是否正确交互与 Windows 操作系统内核。
ms.assetid: 1E536DE0-071B-4529-B228-DB5DAE71099C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ff62733a6c15f04199e7d14cd07395a8b870338
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371574"
---
# <a name="ddi-compliance-checking"></a>DDI 合规性检查


DDI 符合性检查选项确定驱动程序是否正确交互与 Windows 操作系统内核。

**请注意**此选项才可用从 Windows 8 开始。 从 Windows 8.1，您可以通过选择测试其他规则[激活 DDI 符合性检查 （其他） 选项](#activating-the-ddi-compliance-checking-additional-option)。



| DDI 合规性检查 |
|-------------------------|
|                         |

DDI 符合性检查选项应用相同设备驱动程序接口 (DDI) 用法规则[Static Driver Verifier](static-driver-verifier.md)使用来验证您的驱动程序在所需的 IRQL 对函数进行函数调用或正确获取并释放自旋锁。

如果此选项处于活动状态并且驱动程序验证程序检测到驱动程序违反了某个 DDI 符合性规则，驱动程序验证程序 （与参数 1 等于特定符合性规则的标识符) 问题 bug 检查 0xC4。

选择 DDI 符合性检查选项，将包括以下规则。

[**GuardedRegions** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-guardedregions) （从 Windows 8.1 开始）

[**IoSetCompletionExCompleteIrp** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-iosetcompletionexcompleteirp) （从 Windows 8.1 开始）

[**IrqlApcLte**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlapclte)

[**IrqlDispatch**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqldispatch)

[**IrqlExAllocatePool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexallocatepool)

[**IrqlExApcLte1**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexapclte1)

[**IrqlExApcLte2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[**IrqlExApcLte3**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexapclte3)

[**IrqlExPassive**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexpassive)

[**IrqlIoApcLte**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlioapclte)

[**IrqlIoDispatch**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliodispatch)

[**IrqlIoPassive1**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliopassive1)

[**IrqlIoPassive2**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliopassive2)

[**IrqlIoPassive3**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliopassive3)

[**IrqlIoPassive4**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliopassive4)

[**IrqlIoPassive5**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliopassive5)

[**IrqlKeApcLte1**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkeapclte1)

[**IrqlKeApcLte2**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkeapclte2)

[**IrqlKeDispatchLte**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkedispatchlte)

[**IrqlKeReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkereleasespinlock)

[**IrqlKeSetEvent**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkesetevent)

[**IrqlMmApcLte**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlmmapclte)

[**IrqlMmDispatch**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlmmdispatch)

[**IrqlObPassive**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlobpassive)

[**IrqlPsPassive**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlpspassive)

[**IrqlReturn** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlreturn) （从 Windows 8.1 开始）

[**IrqlRtlPassive**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlrtlpassive)

[**IrqlZwPassive**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlzwpassive)

[**NdisOidComplete** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndisoidcomplete) （从 Windows 8.1 开始）

[**NdisOidDoubleComplete** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndisoiddoublecomplete) （从 Windows 8.1 开始）

[**PnpRemove** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-pnpremove) （从 Windows 8.1 开始）

[**RequestedPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-requestedpowerirp) （从 Windows 8.1 开始）

[**QueuedSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-queuedspinlock) （从 Windows 8.1 开始）

[**旋转锁**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-spinlock) （从 Windows 8.1 开始）

## <a name="span-idactivatingtheddicompliancecheckingoptionspanspan-idactivatingtheddicompliancecheckingoptionspanspan-idactivatingtheddicompliancecheckingoptionspanactivating-the-ddi-compliance-checking-option"></a><span id="Activating_the_DDI_compliance_checking_option"></span><span id="activating_the_ddi_compliance_checking_option"></span><span id="ACTIVATING_THE_DDI_COMPLIANCE_CHECKING_OPTION"></span>激活 DDI 符合性检查选项


您可以激活 DDI 符合性检查功能的一个或多个驱动程序使用驱动程序验证程序管理器或 Verifier.exe 命令行。 有关详细信息，请参阅[选择 Driver Verifier 选项](selecting-driver-verifier-options.md)。 必须重新启动计算机以激活或停用 DDI 符合性检查选项。 使用标准设置，将激活 DDI 符合性检查功能 ( **/标准**)。

-   **在命令行**

    在命令行中，在由表示 DDI 符合性检查**verifier /flags 0x00020000** (位 17)。 若要激活 DDI 符合性检查，使用 0x00020000 标志值，或将 0x00020000 添加到标志值。 例如：

    ```
    verifier /flags 0x00020000 /driver MyDriver.sys
    ```

    在下一次启动后，该功能将处于活动状态。

-   **使用驱动程序验证程序管理器**

    1.  启动驱动程序验证器管理器。 类型**Verifier**在命令提示符窗口中。
    2.  选择**创建自定义设置 （适用于代码开发人员）** ，然后单击**下一步**。
    3.  选择**从完整的列表中选择单个设置**。
    4.  选择 （选中） **DDI 符合性检查**。
    5.  重新启动计算机。

## <span id="DDI_compliance_checking_additional"></span><span id="ddi_compliance_checking_additional"></span><span id="DDI_COMPLIANCE_CHECKING_ADDITIONAL"></span>


| DDI 符合性检查 （其他） |
|--------------------------------------|
|                                      |

在 Windows 8.1 中启动**DDI 符合性检查 （其他） 选项**选项提供了其他规则以确定驱动程序是否正确交互与 Windows 操作系统内核。 当选择**DDI 符合性检查 （其他） 选项**，测试以下规则：

-   [**CriticalRegions**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-criticalregions)

-   [**QueuedSpinLockRelease**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-queuedspinlockrelease)

-   [**SpinlockRelease**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-spinlockrelease)

## <a name="activating-the-ddi-compliance-checking-additional-option"></a>激活 DDI 符合性检查 （其他） 的选项


可以激活**DDI 符合性检查 （其他）** 使用驱动程序验证程序管理器或 Verifier.exe 命令行的一个或多个驱动程序的规则。 有关详细信息，请参阅[选择 Driver Verifier 选项](selecting-driver-verifier-options.md)。 必须重新启动计算机以激活或停用**DDI 符合性检查 （其他）** 选项。

-   **在命令行**

    在命令行中，在由表示 DDI 符合性检查**verifier /flags 0x00080000** (位 19)。 若要激活**DDI 符合性检查 （其他）** 、 使用 0x00080000 标志值或将 0x00080000 添加到标志值。 例如：

    ```
    verifier /flags 0x00080000 /driver MyDriver.sys
    ```

    在下一次启动后，该功能将处于活动状态。

-   **使用驱动程序验证程序管理器**

    1.  启动驱动程序验证器管理器。 类型**Verifier**在命令提示符窗口中。
    2.  选择**创建自定义设置 （适用于代码开发人员）** ，然后单击**下一步**。
    3.  选择**从完整的列表中选择单个设置**。
    4.  选择 （选中） **DDI 符合性检查 （其他）** 。
    5.  重新启动计算机。









