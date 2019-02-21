---
title: DDI 符合性检查
description: DDI 符合性检查选项确定驱动程序是否正确交互与 Windows 操作系统内核。
ms.assetid: 1E536DE0-071B-4529-B228-DB5DAE71099C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2293fc4dec72244756870dc8bbfdd3ea19c1b608
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545679"
---
# <a name="ddi-compliance-checking"></a>DDI 符合性检查


DDI 符合性检查选项确定驱动程序是否正确交互与 Windows 操作系统内核。

**请注意**此选项才可用从 Windows 8 开始。 从 Windows 8.1，您可以通过选择测试其他规则[激活 DDI 符合性检查 （其他） 选项](#activating-the-ddi-compliance-checking-additional-option)。



| DDI 符合性检查 |
|-------------------------|
|                         |

DDI 符合性检查选项应用相同设备驱动程序接口 (DDI) 用法规则[Static Driver Verifier](static-driver-verifier.md)使用来验证您的驱动程序在所需的 IRQL 对函数进行函数调用或正确获取并释放自旋锁。

如果此选项处于活动状态并且驱动程序验证程序检测到驱动程序违反了某个 DDI 符合性规则，驱动程序验证程序 （与参数 1 等于特定符合性规则的标识符) 问题 bug 检查 0xC4。

选择 DDI 符合性检查选项，将包括以下规则。

[**GuardedRegions** ](https://msdn.microsoft.com/library/windows/hardware/hh975150) （从 Windows 8.1 开始）

[**IoSetCompletionExCompleteIrp** ](https://msdn.microsoft.com/library/windows/hardware/hh975178) （从 Windows 8.1 开始）

[**IrqlApcLte**](https://msdn.microsoft.com/library/windows/hardware/ff547740)

[**IrqlDispatch**](https://msdn.microsoft.com/library/windows/hardware/ff547743)

[**IrqlExAllocatePool**](https://msdn.microsoft.com/library/windows/hardware/ff547747)

[**IrqlExApcLte1**](https://msdn.microsoft.com/library/windows/hardware/ff547748)

[**IrqlExApcLte2**](https://msdn.microsoft.com/library/windows/hardware/ff547751)

[**IrqlExApcLte3**](https://msdn.microsoft.com/library/windows/hardware/ff547753)

[**IrqlExPassive**](https://msdn.microsoft.com/library/windows/hardware/ff547756)

[**IrqlIoApcLte**](https://msdn.microsoft.com/library/windows/hardware/ff547759)

[**IrqlIoDispatch**](https://msdn.microsoft.com/library/windows/hardware/jj157234)

[**IrqlIoPassive1**](https://msdn.microsoft.com/library/windows/hardware/ff547763)

[**IrqlIoPassive2**](https://msdn.microsoft.com/library/windows/hardware/ff547766)

[**IrqlIoPassive3**](https://msdn.microsoft.com/library/windows/hardware/ff547780)

[**IrqlIoPassive4**](https://msdn.microsoft.com/library/windows/hardware/ff547787)

[**IrqlIoPassive5**](https://msdn.microsoft.com/library/windows/hardware/ff547796)

[**IrqlKeApcLte1**](https://msdn.microsoft.com/library/windows/hardware/ff547803)

[**IrqlKeApcLte2**](https://msdn.microsoft.com/library/windows/hardware/ff547806)

[**IrqlKeDispatchLte**](https://msdn.microsoft.com/library/windows/hardware/ff547812)

[**IrqlKeReleaseSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff547830)

[**IrqlKeSetEvent**](https://msdn.microsoft.com/library/windows/hardware/ff547835)

[**IrqlMmApcLte**](https://msdn.microsoft.com/library/windows/hardware/ff547855)

[**IrqlMmDispatch**](https://msdn.microsoft.com/library/windows/hardware/hh975186)

[**IrqlObPassive**](https://msdn.microsoft.com/library/windows/hardware/ff547873)

[**IrqlPsPassive**](https://msdn.microsoft.com/library/windows/hardware/ff547882)

[**IrqlReturn** ](https://msdn.microsoft.com/library/windows/hardware/ff547886) （从 Windows 8.1 开始）

[**IrqlRtlPassive**](https://msdn.microsoft.com/library/windows/hardware/ff547893)

[**IrqlZwPassive**](https://msdn.microsoft.com/library/windows/hardware/ff547897)

[**NdisOidComplete** ](https://msdn.microsoft.com/library/windows/hardware/dn305115) （从 Windows 8.1 开始）

[**NdisOidDoubleComplete** ](https://msdn.microsoft.com/library/windows/hardware/dn305116) （从 Windows 8.1 开始）

[**PnpRemove** ](https://msdn.microsoft.com/library/windows/hardware/dn322052) （从 Windows 8.1 开始）

[**RequestedPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff551613) （从 Windows 8.1 开始）

[**QueuedSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551494) （从 Windows 8.1 开始）

[**旋转锁**](https://msdn.microsoft.com/library/windows/hardware/ff551861) （从 Windows 8.1 开始）

## <a name="span-idactivatingtheddicompliancecheckingoptionspanspan-idactivatingtheddicompliancecheckingoptionspanspan-idactivatingtheddicompliancecheckingoptionspanactivating-the-ddi-compliance-checking-option"></a><span id="Activating_the_DDI_compliance_checking_option"></span><span id="activating_the_ddi_compliance_checking_option"></span><span id="ACTIVATING_THE_DDI_COMPLIANCE_CHECKING_OPTION"></span>激活 DDI 符合性检查选项


您可以激活 DDI 符合性检查功能的一个或多个驱动程序使用驱动程序验证程序管理器或 Verifier.exe 命令行。 有关详细信息，请参阅[选择 Driver Verifier 选项](selecting-driver-verifier-options.md)。 必须重新启动计算机以激活或停用 DDI 符合性检查选项。 使用标准设置，将激活 DDI 符合性检查功能 (**/标准**)。

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

-   [**CriticalRegions**](https://msdn.microsoft.com/library/windows/hardware/ff543603)

-   [**QueuedSpinLockRelease**](https://msdn.microsoft.com/library/windows/hardware/ff551496)

-   [**SpinlockRelease**](https://msdn.microsoft.com/library/windows/hardware/ff552780)

## <a name="activating-the-ddi-compliance-checking-additional-option"></a>激活 DDI 符合性检查 （其他） 的选项


可以激活**DDI 符合性检查 （其他）** 使用驱动程序验证程序管理器或 Verifier.exe 命令行的一个或多个驱动程序的规则。 有关详细信息，请参阅[选择 Driver Verifier 选项](selecting-driver-verifier-options.md)。 必须重新启动计算机以激活或停用**DDI 符合性检查 （其他）** 选项。

-   **在命令行**

    在命令行中，在由表示 DDI 符合性检查**verifier /flags 0x00080000** (位 19)。 若要激活**DDI 符合性检查 （其他）**、 使用 0x00080000 标志值或将 0x00080000 添加到标志值。 例如：

    ```
    verifier /flags 0x00080000 /driver MyDriver.sys
    ```

    在下一次启动后，该功能将处于活动状态。

-   **使用驱动程序验证程序管理器**

    1.  启动驱动程序验证器管理器。 类型**Verifier**在命令提示符窗口中。
    2.  选择**创建自定义设置 （适用于代码开发人员）** ，然后单击**下一步**。
    3.  选择**从完整的列表中选择单个设置**。
    4.  选择 （选中） **DDI 符合性检查 （其他）**。
    5.  重新启动计算机。









