---
title: DDI 合规性检查
description: DDI 相容性检查选项确定驱动程序是否正确与 Windows 操作系统内核交互。
ms.assetid: 1E536DE0-071B-4529-B228-DB5DAE71099C
ms.date: 04/03/2020
ms.localizationpriority: medium
ms.openlocfilehash: d42be38216c925e45614a01cf6a8a15bcead9a27
ms.sourcegitcommit: 84be9e06fd0886598df77dffcbc75632d613c8f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/11/2020
ms.locfileid: "81217169"
---
# <a name="ddi-compliance-checking"></a>DDI 合规性检查

DDI 相容性检查选项确定驱动程序是否正确与 Windows 操作系统内核交互。

**注意** 从 Windows 8 开始可以使用此选项。 从 Windows 8.1 开始，你可以通过选择["激活 DDI 相容性检查（其他）" 选项](#activating-the-ddi-compliance-checking-additional-option)来测试其他规则。

| DDI 合规性检查 |
|-------------------------|
|                         |

"DDI 相容性检查" 选项应用[静态驱动程序验证](static-driver-verifier.md)器用于验证驱动程序是否在函数所需的 IRQL 上进行函数调用，或正确获取和释放旋转锁的相同设备驱动程序接口（DDI）使用规则。

如果此选项处于活动状态，并且驱动程序验证器检测到该驱动程序违反了某一 DDI 符合性规则，则驱动程序验证程序问题 bug 检查0xC4 （参数1等于特定符合性规则的标识符）。

选择 "DDI 相容性检查" 选项时，将包含以下规则。

[**GuardedRegions**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-guardedregions) （从 Windows 8.1 开始）

[**IoSetCompletionExCompleteIrp**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-iosetcompletionexcompleteirp) （从 Windows 8.1 开始）

[**IrqlApcLte**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlapclte)

[**IrqlDispatch**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqldispatch)

[**IrqlExAllocatePool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexallocatepool)

[**IrqlExApcLte1**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexapclte1)

[**IrqlExApcLte2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

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

[**IrqlReturn**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlreturn) （从 Windows 8.1 开始）

[**IrqlRtlPassive**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlrtlpassive)

[**IrqlZwPassive**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlzwpassive)

[**NdisOidComplete**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndisoidcomplete) （从 Windows 8.1 开始）

[**NdisOidDoubleComplete**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndisoiddoublecomplete) （从 Windows 8.1 开始）

[**PnpRemove**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-pnpremove) （从 Windows 8.1 开始）

[**RequestedPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-requestedpowerirp) （从 Windows 8.1 开始）

[**QueuedSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-queuedspinlock) （从 Windows 8.1 开始）

[**旋转锁**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-spinlock)（从 Windows 8.1 开始）

这两个规则当前是可选的，但建议这样做。

[可有可无**IrqlNtifsApcPassive**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlntifsapcpassive)

[可有可无**IrqlIoRtlZwPassive**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliortlzwpassive)

## <a name="span-idactivating_the_ddi_compliance_checking_optionspanspan-idactivating_the_ddi_compliance_checking_optionspanspan-idactivating_the_ddi_compliance_checking_optionspanactivating-the-ddi-compliance-checking-option"></a><span id="Activating_the_DDI_compliance_checking_option"></span><span id="activating_the_ddi_compliance_checking_option"></span><span id="ACTIVATING_THE_DDI_COMPLIANCE_CHECKING_OPTION"></span>激活 DDI 相容性检查选项

您可以使用驱动程序验证器管理器或 Verifier 命令行为一个或多个驱动程序激活 DDI 相容性检查功能。 有关详细信息，请参阅[选择驱动程序验证程序选项](selecting-driver-verifier-options.md)。 您必须重新启动计算机以激活或停用 DDI 相容性检查选项。 当你使用标准设置（ **/标准**）时，将激活 DDI 相容性检查功能。

-   **在命令行中**

    在命令行中，DDI 相容性检查由**verifier/flags 0x00020000** （第17位）表示。 若要激活 DDI 相容性检查，请使用0x00020000 的标志值或将0x00020000 添加到标志值。 例如：

    ```
    verifier /flags 0x00020000 /driver MyDriver.sys
    ```

    此功能将在下一次启动后处于活动状态。

-   **使用驱动程序验证器管理器**

    1.  启动驱动程序验证器管理器。 在命令提示符窗口中键入**Verifier** 。
    2.  选择 "**创建自定义设置（对于代码开发人员）** "，然后单击 "**下一步**"。
    3.  选择 "**从完整列表中选择单个设置**"。
    4.  选择（检查） **DDI 相容性检查**。
    5.  重启计算机。

## <span id="DDI_compliance_checking_additional"></span><span id="ddi_compliance_checking_additional"></span><span id="DDI_COMPLIANCE_CHECKING_ADDITIONAL"></span>


| DDI 相容性检查（其他） |
|--------------------------------------|
|                                      |

从 Windows 8.1 开始， **DDI 相容性检查（附加）选项**选项提供其他规则来确定驱动程序是否与 Windows 操作系统内核正确交互。 如果选择 " **DDI 相容性检查（其他）" 选项**，则测试以下规则：

- [**CriticalRegions**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-criticalregions)

- [**QueuedSpinLockRelease**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-queuedspinlockrelease)

- [**SpinlockRelease**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-spinlockrelease)

## <a name="activating-the-ddi-compliance-checking-additional-option"></a>激活 "DDI 相容性检查（其他）" 选项

您可以使用驱动程序验证器管理器或 Verifier 命令行为一个或多个驱动程序激活**DDI 相容性检查（其他）** 规则。 有关详细信息，请参阅[选择驱动程序验证程序选项](selecting-driver-verifier-options.md)。 您必须重新启动计算机以激活或停用**DDI 相容性检查（其他）** 选项。

-   **在命令行中**

    在命令行中，DDI 相容性检查由**verifier/flags 0x00080000** （位19）表示。 若要激活**DDI 相容性检查（其他）** ，请使用0x00080000 的标志值或将0x00080000 添加到标志值。 例如：

    ```
    verifier /flags 0x00080000 /driver MyDriver.sys
    ```

    此功能将在下一次启动后处于活动状态。

-   **使用驱动程序验证器管理器**

    1.  若要启动驱动程序验证程序管理器，请在命令提示符窗口中键入**Verifier** 。
    2.  选择 "**创建自定义设置（对于代码开发人员）** "，然后单击 "**下一步**"。
    3.  选择 "**从完整列表中选择单个设置**"。
    4.  选择（检查） **DDI 相容性检查（其他）** 。
    5.  重启计算机。

## <a name="activating-the-ddi-compliance-checking-additional-irql-option"></a>激活 DDI 相容性检查（其他 IRQL）选项

您可以使用 Verifier 命令行为一个或多个驱动程序激活 DDI 相容性其他 IRQL 规则。 有关详细信息，请参阅[选择驱动程序验证程序选项](selecting-driver-verifier-options.md)。 您必须重新启动计算机以激活或停用 DDI 相容性其他 IRQL 规则。

在命令行中，DDI 相容性附加的 IRQL 检查用规则类值35表示。 例如：

`verifier /ruleclasses 35 /driver MyDriver.sys`

或者

`verifier /rc 35 /driver MyDriver.sys`

其他 IRQL 规则集包含以下两个规则。

[可有可无**IrqlNtifsApcPassive**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlntifsapcpassive)

[可有可无**IrqlIoRtlZwPassive**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliortlzwpassive)


