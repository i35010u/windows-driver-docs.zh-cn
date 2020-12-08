---
title: I/O 验证
description: I/O 验证
keywords:
- I/o 验证功能 WDK 驱动程序验证程序
- 1级 i/o 验证 WDK 驱动程序验证程序
- 级别 2 i/o 验证 WDK 驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 026b9f4cda46e47ebbca5e187a2cf078f2e3342d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824643"
---
# <a name="io-verification"></a>I/O 验证


## <span id="ddk_i_o_verification_tools"></span><span id="DDK_I_O_VERIFICATION_TOOLS"></span>


驱动程序验证程序有两个级别的 i/o 验证：

-   *第1级 I/o 验证* 始终处于活动状态，只要选择了 i/o 验证。

-   如果在 Windows XP 和更高版本中选择了 i/o 验证，则 *第2级 I/o 验证* 始终处于活动状态。 在 Windows 2000 中，可以将 i/o 验证配置为同时包含这两个级别，或仅包括1级测试。

**另请参阅：** windows 7 和更高版本的 windows 操作系统中的 [增强 i/o 验证](enhanced-i-o-verification.md) ，当你选择 "i/o 验证" 时，将自动激活增强的 i/o 验证。 不能将其选择为单独的选项。

### <a name="span-idlevel_1_i_o_verificationspanspan-idlevel_1_i_o_verificationspanlevel-1-io-verification"></a><span id="level_1_i_o_verification"></span><span id="LEVEL_1_I_O_VERIFICATION"></span>1级 i/o 验证

启用级别 1 i/o 验证后，通过 **IoAllocateIrp** 获取的所有 irp 都将从特殊池分配，并跟踪其使用情况。

此外，驱动程序验证器还会检查是否存在无效的 i/o 调用，其中包括：

-   尝试释放其类型不是 IO \_ 类型 irp 的 irp \_

-   将无效设备对象传递到 **IoCallDriver**

-   将 IRP 传递到包含无效状态或仍具有取消例程集的 **IoCompleteRequest**

-   通过对驱动程序调度例程的调用来更改 IRQL

-   尝试释放与线程关联的 IRP

-   将设备对象传递到已包含已初始化计时器的 **IoInitializeTimer**

-   将无效缓冲区传递到 **IoBuildAsynchronousFsdRequest** 或 **IoBuildDeviceIoControlRequest**

-   将 i/o 状态块传递给 IRP，当此 i/o 状态块在展开过远的堆栈上分配时

-   当此事件对象在展开过远的堆栈上分配时，将事件对象传递给 IRP

由于特殊 IRP 池的大小有限，因此，当一次仅在一个驱动程序上使用时，i/o 验证将最有效。

I/o 验证级别1失败导致发出 bug 检查0xC9。 此错误检查的第一个参数指示发生了什么冲突。 有关完整参数列表，请参阅 [**Bug 检查 0xC9**](../debugger/bug-check-0xc9--driver-verifier-iomanager-violation.md) (DRIVER \_ VERIFIER \_ IOMANAGER \_ 违例) 。

### <a name="span-idlevel_2_i_o_verificationspanspan-idlevel_2_i_o_verificationspanlevel-2-io-verification"></a><span id="level_2_i_o_verification"></span><span id="LEVEL_2_I_O_VERIFICATION"></span>2级 i/o 验证

I/o 验证级别2错误以不同方式显示：在蓝屏上、崩溃转储文件和内核调试器中。

在蓝屏上，消息 **IO 系统验证错误** 和字符串 **WDM 驱动程序错误**_XXX_ 指出了这些错误，其中 *XXX* 是 i/o 错误代码。

在崩溃转储文件中，其中的大多数错误都记录在消息 **错误检查 0xC9 (DRIVER \_ VERIFIER \_ IOMANAGER \_ 违例)**，以及 i/o 错误代码。 在这种情况下，i/o 错误代码将显示为 bug 检查0xC9 的第一个参数。 其余部分由消息 **错误检查 0xC4 (驱动程序验证程序 \_ \_ 检测到 \_ 冲突)**，以及驱动程序验证程序错误代码。 在这种情况下，驱动程序验证程序错误代码将显示为 bug 检查0xC4 的第一个参数。

在 (KD 或 WinDbg) 的内核调试器中，消息 **WDM 驱动程序错误** 和描述性文本字符串指出了这些错误。 当内核调试器处于活动状态时，可以忽略第2级错误并恢复系统操作。  (在任何其他 bug 检查中都不可能。 ) 

蓝屏、故障转储文件和内核调试器也会显示附加信息。 有关大多数 i/o 验证级别2错误消息的完整说明，请参阅 [**Bug 检查 0xC9**](../debugger/bug-check-0xc9--driver-verifier-iomanager-violation.md)。 有关剩余部分，请参阅 [**Bug 检查 0xC4**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md)。

从 Windows Vista 开始，i/o 验证选项会检查是否存在以下驱动程序错误：

-   在用户模式应用程序中完成和取消 Irp 需要的时间太长。

-   正在释放尚未获取的删除锁定。

-   使用与相应 [**IoAcquireRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)调用中使用的 tag 参数不同的 tag 参数调用 [**IoReleaseRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)或 [**IoReleaseRemoveLockAndWait**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait) 。

-   调用已禁用中断的 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 。

-   调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 的 IRQL 大于调度 \_ 级别。

-   从已禁用中断的驱动程序调度例程中返回。

-   从具有更改的 IRQL 的驱动程序调度例程返回。

-   从已禁用 Apc 的驱动程序调度例程返回。 在这种情况下，驱动程序的调用次数可能比 [**KeLeaveCriticalRegion**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)多 [**KeEnterCriticalRegion**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion) ，这是在 [**Bug Check 0x20**](../debugger/bug-check-0x20--kernel-apc-pending-during-exit.md) \_ \_ \_ \_ EXIT) 和 [**bug 检查 0X1**](../debugger/bug-check-0x1--apc-index-mismatch.md) (APC \_ 索引 \_ 不) 匹配时，出现错误检查 (0x20 的主要原因。

从 Windows 7 开始，i/o 验证选项会检查是否存在以下驱动程序错误：

-   尝试通过调用 [**ExFreePool**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)来释放 irp。 必须用 [**IoFreeIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)释放 irp。

此外，还可以使用此选项检测另一个常见的驱动程序错误，即重新初始化删除锁。 应在设备扩展内分配 "删除锁" 数据结构。 这可确保 \_ \_ 只有在删除设备对象时，i/o 管理器才会释放保存 IO 删除锁定结构的内存。 如果驱动程序执行以下三个步骤，则可能在步骤2之后，应用程序或驱动程序仍保留对 Device1 的引用：

-   分配 \_ \_ 对应于 DEVICE1 的 IO 删除锁结构，但在 Device1's 扩展外进行分配。
-   删除 Device1 时调用 [**IoReleaseRemoveLockAndWait**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait) 。
-   为同一个锁调用 [**IoInitializeRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializeremovelock) ，以将其用作设备2的删除锁定。

在步骤2之后，应用程序或驱动程序可能仍持有对 Device1 的引用。 即使删除了此设备，应用程序或驱动程序仍可以向 Device1 发送请求。 因此，在 i/o 管理器删除 Device1 之前，不安全地重复使用同一内存作为新的删除锁定。 如果在另一个线程尝试获取同一个锁时重新初始化该锁，则可能会导致锁定损坏，并导致驱动程序和整个系统产生不可预知的结果。

在 windows 7 和更高版本的 Windows 操作系统中，当你选择 "i/o 验证" 时，将自动激活 [增强的 I/o 验证](enhanced-i-o-verification.md) 。

### <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项

你可以通过使用驱动程序验证器管理器或 Verifier.exe 命令行来激活一个或多个驱动程序的 i/o 验证功能。 有关详细信息，请参阅 [选择驱动程序验证程序选项](selecting-driver-verifier-options.md)。

-   **在命令行中。**

    在命令行中，i/o 验证选项由 **第4个 (0x10)** 表示。 若要激活 i/o 验证，请使用值为0x10 的标志值或将0x10 添加到标志值。 例如：

    ```
    verifier /flags 0x10 /driver MyDriver.sys
    ```

    此功能将在下一次启动后处于活动状态。

    在 Windows 2000 中，可以使用 **/iolevel** 参数仅激活默认)  (级别1和级别2。 在更高版本的 Windows 中，当你激活 i/o 验证时，级别1和级别2始终都会激活。

    例如，以下命令将在运行 Windows 2000 的计算机上激活级别1和级别 2 i/o 验证。

    ```
    verifier /flags 0x10 /iolevel 2 /driver MyDriver.sys
    ```

    在 Windows Vista 和更高版本的 Windows 上，还可以通过将 **/volatile** 参数添加到命令来激活和停用 i/o 验证，而无需重新启动计算机。 例如：

    ```
    verifier /volatile /flags 0x10 /adddriver MyDriver.sys
    ```

    此设置将立即生效，但当你关闭或重新启动计算机时，此设置会丢失。 有关详细信息，请参阅 [使用可变设置](using-volatile-settings.md)。

    标准设置中也包含 i/o 验证功能。 例如：

    ```
    verifier /standard /driver MyDriver.sys
    ```

-   **使用驱动程序验证器管理器**

    1.  选择 " **为代码开发人员 (创建自定义设置")** ，然后单击 " **下一步**"。
    2.  选择 " **从完整列表中选择单个设置**"。
    3.  选择 (检查) **i/o 验证**。

    标准设置中也包含 i/o 验证功能。 若要使用此功能，请在驱动程序验证器管理器中单击 " **创建标准设置**"。

 

