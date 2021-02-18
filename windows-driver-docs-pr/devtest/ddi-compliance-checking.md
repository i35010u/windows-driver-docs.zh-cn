---
title: DDI 合规性检查
description: DDI 相容性检查选项确定驱动程序是否正确与 Windows 操作系统内核交互。
ms.date: 04/03/2020
ms.localizationpriority: medium
ms.openlocfilehash: ca6d70ce0e54d87c9225a7a8a504c19a7eb0f200
ms.sourcegitcommit: 20569e032b1e0963ad295e9c46b7682832af3d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/18/2021
ms.locfileid: "100648168"
---
# <a name="ddi-compliance-checking"></a>DDI 合规性检查

DDI 相容性检查选项确定驱动程序是否正确与 Windows 操作系统内核交互。

**注意**  从 Windows 8 开始可以使用此选项。 从 Windows 8.1 开始，你可以通过选择 ["激活 DDI 相容性检查" (其他) 选项](#activating-the-ddi-compliance-checking-additional-option)来测试其他规则。

| DDI 合规性检查 |
|-------------------------|
|                         |

DDI 相容性检查选项应用 (DDI) 使用规则的相同设备驱动程序接口， [静态驱动程序验证](static-driver-verifier.md) 器使用这些规则来验证驱动程序是否在函数所需的 IRQL 上发出函数调用，或正确获取和释放旋转锁。

如果此选项处于活动状态，并且驱动程序验证器检测到该驱动程序违反了某个 DDI 符合性规则，则驱动程序验证程序问题会检查 0xC4 (参数1等于特定符合性规则的标识符) 。

选择 "DDI 相容性检查" 选项时，将包含以下规则。

[**GuardedRegions**](./wdm-guardedregions.md) (Windows 8.1) 

[**IoSetCompletionExCompleteIrp**](./wdm-iosetcompletionexcompleteirp.md) (Windows 8.1) 

[**IrqlApcLte**](./wdm-irqlapclte.md)

[**IrqlDispatch**](./wdm-irqldispatch.md)

[**IrqlExAllocatePool**](./wdm-irqlexallocatepool.md)

[**IrqlExApcLte1**](./wdm-irqlexapclte1.md)

[**IrqlExApcLte2**](./wdm-irqlexapclte2.md)

[**IrqlExApcLte3**](./wdm-irqlexapclte3.md)

[**IrqlExPassive**](./wdm-irqlexpassive.md)

[**IrqlIoApcLte**](./wdm-irqlioapclte.md)

[**IrqlIoDispatch**](./wdm-irqliodispatch.md)

[**IrqlIoPassive1**](./wdm-irqliopassive1.md)

[**IrqlIoPassive2**](./wdm-irqliopassive2.md)

[**IrqlIoPassive3**](./wdm-irqliopassive3.md)

[**IrqlIoPassive4**](./wdm-irqliopassive4.md)

[**IrqlIoPassive5**](./wdm-irqliopassive5.md)

[**IrqlKeApcLte1**](./wdm-irqlkeapclte1.md)

[**IrqlKeApcLte2**](./wdm-irqlkeapclte2.md)

[**IrqlKeDispatchLte**](./wdm-irqlkedispatchlte.md)

[**IrqlKeReleaseSpinLock**](./wdm-irqlkereleasespinlock.md)

[**IrqlKeSetEvent**](./wdm-irqlkesetevent.md)

[**IrqlMmApcLte**](./wdm-irqlmmapclte.md)

[**IrqlMmDispatch**](./wdm-irqlmmdispatch.md)

[**IrqlObPassive**](./wdm-irqlobpassive.md)

[**IrqlPsPassive**](./wdm-irqlpspassive.md)

[**IrqlReturn**](./wdm-irqlreturn.md) (Windows 8.1) 

[**IrqlRtlPassive**](./wdm-irqlrtlpassive.md)

[**IrqlZwPassive**](./wdm-irqlzwpassive.md)

[**NdisOidComplete**](./ndis-ndisoidcomplete.md) (Windows 8.1) 

[**NdisOidDoubleComplete**](./ndis-ndisoiddoublecomplete.md) (Windows 8.1) 

[**PnpRemove**](./wdm-pnpremove.md) (Windows 8.1) 

[**RequestedPowerIrp**](./wdm-requestedpowerirp.md) (Windows 8.1) 

[**QueuedSpinLock**](./wdm-queuedspinlock.md) (Windows 8.1) 

[**旋转锁**](./wdm-spinlock.md) (Windows 8.1) 

这两个规则当前是可选的，但建议这样做。

[ (可选) **IrqlNtifsApcPassive**](./wdm-irqlntifsapcpassive.md)

[ (可选) **IrqlIoRtlZwPassive**](./wdm-irqliortlzwpassive.md)

## <a name="span-idactivating_the_ddi_compliance_checking_optionspanspan-idactivating_the_ddi_compliance_checking_optionspanspan-idactivating_the_ddi_compliance_checking_optionspanactivating-the-ddi-compliance-checking-option"></a><span id="Activating_the_DDI_compliance_checking_option"></span><span id="activating_the_ddi_compliance_checking_option"></span><span id="ACTIVATING_THE_DDI_COMPLIANCE_CHECKING_OPTION"></span>激活 DDI 相容性检查选项

您可以使用驱动程序验证器管理器或 Verifier.exe 命令行为一个或多个驱动程序激活 DDI 相容性检查功能。 有关详细信息，请参阅 [选择驱动程序验证程序选项](selecting-driver-verifier-options.md)。 您必须重新启动计算机以激活或停用 DDI 相容性检查选项。 使用标准设置 (**/标准**) 时，会激活 DDI 相容性检查功能。

-   **在命令行中**

    在命令行中，DDI 相容性检查由 **verifier/flags 0x00020000** (位 17) 表示。 若要激活 DDI 相容性检查，请使用0x00020000 的标志值或将0x00020000 添加到标志值。 例如：

    ```
    verifier /flags 0x00020000 /driver MyDriver.sys
    ```

    此功能将在下一次启动后处于活动状态。

-   **使用驱动程序验证器管理器**

    1.  启动驱动程序验证器管理器。 在命令提示符窗口中键入 **Verifier** 。
    2.  选择 " **为代码开发人员 (创建自定义设置")** ，然后单击 " **下一步**"。
    3.  选择 " **从完整列表中选择单个设置**"。
    4.  选择 (检查) **DDI 相容性检查**"。
    5.  重新启动计算机。

## <span id="DDI_compliance_checking_additional"></span><span id="ddi_compliance_checking_additional"></span><span id="DDI_COMPLIANCE_CHECKING_ADDITIONAL"></span>


| DDI 相容性检查 (额外)  |
|--------------------------------------|
|                                      |

从 Windows 8.1 开始， **DDI 相容性检查 (其他) 选项** 选项提供其他规则来确定驱动程序是否与 Windows 操作系统内核正确交互。 选择 " **DDI 相容性检查" (额外的) "选项** 时，将测试以下规则：

- [**CriticalRegions**](./wdm-criticalregions.md)

- [**QueuedSpinLockRelease**](./wdm-queuedspinlockrelease.md)

- [**SpinlockRelease**](./wdm-spinlockrelease.md)

## <a name="activating-the-ddi-compliance-checking-additional-option"></a> (其他) 选项激活 DDI 相容性检查

>[!Note]
> **从 Windows 10 预览体验版本19042及更高版本开始，此检查已弃用**


您可以通过使用驱动程序验证器管理器或 Verifier.exe 命令行，为一个或多个驱动程序激活 **额外) 规则 (DDI 相容性检查** 。 有关详细信息，请参阅 [选择驱动程序验证程序选项](selecting-driver-verifier-options.md)。 您必须重新启动计算机，以激活或停用 **DDI 相容性检查 (其他)** 选项。

-   **在命令行中**

    在命令行中，DDI 相容性检查由 **verifier/flags 0x00080000** (位 19) 表示。 若要激活 **额外)  (的 DDI 相容性检查**，请使用0x00080000 的标志值或将0x00080000 添加到标志值。 例如：

    ```
    verifier /flags 0x00080000 /driver MyDriver.sys
    ```

    此功能将在下一次启动后处于活动状态。

-   **使用驱动程序验证器管理器**

    1.  若要启动驱动程序验证程序管理器，请在命令提示符窗口中键入 **Verifier** 。
    2.  选择 " **为代码开发人员 (创建自定义设置")** ，然后单击 " **下一步**"。
    3.  选择 " **从完整列表中选择单个设置**"。
    4.  选择 (检查) **DDI 相容性检查 (其他)**。
    5.  重新启动计算机。

## <a name="activating-the-ddi-compliance-checking-additional-irql-option"></a>激活 DDI 相容性检查 (额外的 IRQL) 选项

您可以使用 Verifier.exe 命令行为一个或多个驱动程序激活 DDI 相容性附加的 IRQL 规则。 有关详细信息，请参阅 [选择驱动程序验证程序选项](selecting-driver-verifier-options.md)。 您必须重新启动计算机以激活或停用 DDI 相容性其他 IRQL 规则。

在命令行中，DDI 相容性附加的 IRQL 检查用规则类值35表示。 例如：

`verifier /ruleclasses 35 /driver MyDriver.sys`

OR

`verifier /rc 35 /driver MyDriver.sys`

其他 IRQL 规则集包含以下两个规则。

[ (可选) **IrqlNtifsApcPassive**](./wdm-irqlntifsapcpassive.md)

[ (可选) **IrqlIoRtlZwPassive**](./wdm-irqliortlzwpassive.md)