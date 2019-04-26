---
title: I/O 验证
description: I/O 验证
ms.assetid: 41b77bba-fae8-453b-9872-911f5d5be3e6
keywords:
- I/O 验证功能 WDK Driver Verifier
- 级别 1 I/O 验证 WDK 驱动程序验证程序
- 级别 2 I/O 验证 WDK 驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f13e54f873ecdc89622a0298bc258f6709a994b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330646"
---
# <a name="io-verification"></a>I/O 验证


## <span id="ddk_i_o_verification_tools"></span><span id="DDK_I_O_VERIFICATION_TOOLS"></span>


驱动程序验证程序具有两个级别的 I/O 验证：

-   *级别 1 的 I/O 验证*选择 I/O 验证时将始终处于活动。

-   *级别 2 的 I/O 验证*I/O 验证选择 Windows XP 及更高版本时将始终处于活动。 在 Windows 2000 中，可以将 I/O 验证配置为包括这两个级别，或只需 1 级测试。

**另请参阅：**[增强的 I/O 验证](enhanced-i-o-verification.md)在 Windows 7 和更高版本的 Windows 操作系统中，增强的 I/O 验证时，将自动激活选择的 I/O 验证。 它不可用或有必要以选择它作为单独的选项。

### <a name="span-idlevel1ioverificationspanspan-idlevel1ioverificationspanlevel-1-io-verification"></a><span id="level_1_i_o_verification"></span><span id="LEVEL_1_I_O_VERIFICATION"></span>级别 1 I/O 验证

通过启用级别 1 的 I/O 验证后，获取所有 Irp **IoAllocateIrp**从特殊池分配和跟踪其使用。

此外，驱动程序验证程序检查存在无效的 I/O 调用，包括：

-   尝试释放其类型不是 IO IRP\_类型\_IRP

-   传递无效的设备对象与**IoCallDriver**

-   传递到 IRP **IoCompleteRequest** ，其中包含无效的状态或仍具有取消例程集

-   在对驱动程序调度例程的调用之间 IRQL 对更改

-   尝试释放仍与线程相关联的 IRP

-   传递到一个设备对象**最好**已经包含一个已初始化的计时器

-   传递到一个无效的缓冲区**IoBuildAsynchronousFsdRequest**或**IoBuildDeviceIoControlRequest**

-   上有太远展开的堆栈分配该块 I/O 状态时要 IRP，传递的 I/O 状态阻止

-   将事件的对象传递给 IRP 上有太远展开的堆栈, 分配此事件对象时

由于特殊的 IRP 池大小有限制，I/O 验证是最有效，它是仅在一个驱动程序上一次使用时。

1 级的 I/O 验证失败导致 bug 检查 0xC9 要颁发。 此 bug 检查的第一个参数指示发生了哪些冲突。 请参阅[ **Bug 检查 0xC9** ](https://msdn.microsoft.com/library/windows/hardware/ff560205) (驱动程序\_VERIFIER\_IOMANAGER\_冲突) 有关的完整参数列表。

### <a name="span-idlevel2ioverificationspanspan-idlevel2ioverificationspanlevel-2-io-verification"></a><span id="level_2_i_o_verification"></span><span id="LEVEL_2_I_O_VERIFICATION"></span>级别 2 I/O 验证

I/O 验证第 2 级错误都显示在不同的方式： 在蓝色屏幕上，在崩溃转储文件，并在内核调试器中。

在蓝色屏幕上，这些错误进行说明的消息**IO 系统验证错误**和字符串 **WDM 驱动程序错误 * * * XXX*，其中*XXX*是 I/O 错误代码。

在崩溃转储文件中，大多数错误进行说明的消息**检测错误 0xC9 (驱动程序\_VERIFIER\_IOMANAGER\_冲突)**，以及 I/O 错误代码。 在这种情况下，I/O 错误代码显示为 bug 检查 0xC9 的第一个参数。 其余部分所述的消息**Bug 检查 0xC4 (驱动程序\_VERIFIER\_检测到\_冲突)**，以及驱动程序验证程序错误代码。 在这种情况下，驱动程序验证程序错误代码显示为 bug 检查 0xC4 的第一个参数。

在内核调试器 （KD 或 WinDbg） 中，这些错误记录的消息**WDM 驱动程序错误**和说明性文本字符串。 当内核调试程序处于活动状态时，则可以忽略第 2 级错误并继续执行系统操作。 （这是不可能与任何其他 bug 检查。）

蓝色的屏幕、 故障转储文件和内核调试程序每个显示其他信息。 大多数的 I/O 验证第 2 级错误消息的完整说明，请参阅[ **Bug 检查 0xC9**](https://msdn.microsoft.com/library/windows/hardware/ff560205)。 其余部分中，请参阅[ **Bug 检查 0xC4**](https://msdn.microsoft.com/library/windows/hardware/ff560187)。

I/O 验证选项启动 Window Vista 中，检查以下驱动程序错误：

-   时间太长，以完成并取消用户模式应用程序中产生的 Irp。

-   释放尚未获取删除锁。

-   调用[ **IoReleaseRemoveLock** ](https://msdn.microsoft.com/library/windows/hardware/ff549560)或[ **IoReleaseRemoveLockAndWait** ](https://msdn.microsoft.com/library/windows/hardware/ff549567)使用不同于 tag 参数的标记参数使用在相应[ **IoAcquireRemoveLock** ](https://msdn.microsoft.com/library/windows/hardware/ff548204)调用。

-   调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)都会在禁用。

-   调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)在 IRQL 大于调度\_级别。

-   从驱动程序调度例程返回都会在禁用。

-   从与更改的 IRQL 的驱动程序调度例程中返回。

-   从驱动程序调度例程返回与禁用的 Apc。 在这种情况下，该驱动程序可能具有名为[ **KeEnterCriticalRegion** ](https://msdn.microsoft.com/library/windows/hardware/ff552021)多次[ **KeLeaveCriticalRegion**](https://msdn.microsoft.com/library/windows/hardware/ff552964)，这是主要原因[ **Bug 检查 0x20** ](https://msdn.microsoft.com/library/windows/hardware/ff557421) (内核\_APC\_PENDING\_在\_退出) 和[ **Bug 检查 0x1** ](https://msdn.microsoft.com/library/windows/hardware/ff557419) (APC\_索引\_不匹配)。

I/O 验证选项启动 Windows 7 中，检查以下驱动程序错误：

-   尝试通过调用释放 Irp [ **ExFreePool**](https://msdn.microsoft.com/library/windows/hardware/ff544590)。 必须用释放 Irp [ **IoFreeIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549113)。

此外，可以使用此选项来检测另一个常见的驱动程序错误，重新初始化删除锁。 删除数据结构应分配内部设备扩展的锁定。 这可确保在 I/O 管理器释放包含 IO 的内存\_删除\_锁结构仅当已删除的设备对象。 如果该驱动程序将执行以下三个步骤，就可以，在步骤 2 中之后, 的应用程序或驱动程序仍保留设备 1 的引用：

-   分配 IO\_删除\_锁结构，它对应于设备 1，但不分配外部设备 1 的扩展。
-   调用[ **IoReleaseRemoveLockAndWait** ](https://msdn.microsoft.com/library/windows/hardware/ff549567) Device1 中要删除的时间。
-   调用[ **IoInitializeRemoveLock** ](https://msdn.microsoft.com/library/windows/hardware/ff549324)同一个锁来重复使用它作为删除锁定的设备 2。

很可能是，在步骤 2 的应用程序或驱动程序仍保留对设备 1 的引用。 应用程序或驱动程序仍可发送请求到 Device1，即使已删除此设备。 因此，不安全地重复使用作为新的删除锁定的相同内存，直到 I/O 管理器会删除设备 1。 重新初始化同一个锁，而另一个线程尝试获取它可能会导致损坏的锁，该驱动程序和整个系统的结果不可预知。

在 Windows 7 和更高版本的 Windows 操作系统，[增强的 I/O 验证](enhanced-i-o-verification.md)时选择的 I/O 验证自动激活。

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项

可以使用驱动程序验证程序管理器或 Verifier.exe 命令行来激活一个或多个驱动程序的 I/O 验证功能。 有关详细信息，请参阅[选择 Driver Verifier 选项](selecting-driver-verifier-options.md)。

-   **在命令行中。**

    在命令行中，由表示 I/O 验证选项**位 4 (0x10)**。 若要激活的 I/O 验证，使用 0x10 标志值，或将 0x10 添加到标志值。 例如：

    ```
    verifier /flags 0x10 /driver MyDriver.sys
    ```

    在下一次启动后，该功能将处于活动状态。

    在 Windows 2000 中，可以使用 **/iolevel**参数，以激活仅级别 1 （默认值） 或级别 1 和级别 2。 在更高版本的 Windows 中，激活的 I/O 验证时，则始终被激活级别 1 和级别 2。

    例如，以下命令将激活级别 1 和级别 2 I/O 验证运行 Windows 2000 的计算机上。

    ```
    verifier /flags 0x10 /iolevel 2 /driver MyDriver.sys
    ```

    在 Windows Vista 和更高版本的 Windows 上，您可以还激活和停 I/O 验证用而无需重启计算机，通过添加 **/volatile**命令参数。 例如：

    ```
    verifier /volatile /flags 0x10 /adddriver MyDriver.sys
    ```

    此设置将立即生效，但当你关闭或重新启动计算机时将丢失。 有关详细信息，请参阅[使用易失性设置](using-volatile-settings.md)。

    I/O 验证功能也包含在标准设置。 例如：

    ```
    verifier /standard /driver MyDriver.sys
    ```

-   **使用驱动程序验证程序管理器**

    1.  选择**创建自定义设置 （适用于代码开发人员）** ，然后单击**下一步**。
    2.  选择**从完整的列表中选择单个设置**。
    3.  选择 （选中） **I/O 验证**。

    I/O 验证功能也包含在标准设置。 若要使用此功能，驱动程序验证程序管理器中，单击**创建标准设置**。

 

 





