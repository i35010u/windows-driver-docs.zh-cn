---
title: 增强的 I/O 验证
description: 增强的 I/O 验证
ms.assetid: ce8a0b22-fa27-45e5-b013-b3accf604ed4
keywords:
- 增强的 i/o 验证功能 WDK 驱动程序验证程序
- I/o 验证功能 WDK 驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e6f1a4a8b2ec82ab8536fd5130f785c3a12a51f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840267"
---
# <a name="enhanced-io-verification"></a>增强的 I/O 验证


此功能仅在 Windows XP 和更高版本的 Windows 操作系统中可用。

在 windows 7 和更高版本的 Windows 操作系统中，当你选择 "i/o 验证" 时，将自动激活增强的 i/o 验证。 不能将其选择为单独的选项。

当增强的 i/o 验证被激活时，Driver Verifier 会监视多个 i/o 管理器例程的调用，并对 PnP Irp、电源 Irp 和 WMI Irp 执行压力测试。

在 Windows Vista 和 Windows XP 中，增强的 i/o 验证会独立于[I/o 验证](i-o-verification.md)被激活，但同时选择这两个选项可为驱动程序中的 i/o 接口方法提供更完整的测试。

### <a name="span-idfeatures_of_enhanced_i_o_verificationspanspan-idfeatures_of_enhanced_i_o_verificationspanfeatures-of-enhanced-io-verification"></a><span id="features_of_enhanced_i_o_verification"></span><span id="FEATURES_OF_ENHANCED_I_O_VERIFICATION"></span>增强的 i/o 验证功能

当激活增强的 i/o 验证时，驱动程序验证器会添加下列检查。

-   监视所有 Irp，以确保驱动程序返回状态\_当且仅当它已调用[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)时才会返回。

-   监视[**IoDeleteDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)的使用情况，验证驱动程序是否不会多次删除相同的设备，并且无法检测不适当的设备对象分离和删除。

-   验证驱动程序是否正确地展开了所有[**IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)调用。

新的强调和测试包括：

-   打乱枚举设备的顺序，以确保即插即用（PnP）驱动程序不会对设备启动顺序作出假设。

-   在 PnP 和电源 Irp 完成后调整其状态，以捕获从其调度例程返回错误状态的驱动程序。

-   发送虚假电源 Irp 来测试驱动程序代码路径 bug。

-   发送伪 WMI Irp 来测试驱动程序代码路径 bug。

-   将一个虚设筛选器插入到每个 WDM 堆栈中。

### <a name="span-iddisplaying_enhanced_i_o_verification_errorsspanspan-iddisplaying_enhanced_i_o_verification_errorsspandisplaying-enhanced-io-verification-errors"></a><span id="displaying_enhanced_i_o_verification_errors"></span><span id="DISPLAYING_ENHANCED_I_O_VERIFICATION_ERRORS"></span>显示增强的 i/o 验证错误

增强型 i/o 验证捕获的驱动程序错误的显示方式与[级别 2 I/o 验证](i-o-verification.md)所捕获的驱动程序错误相同。

在蓝屏上，消息**IO 系统验证错误**和字符串**WDM 驱动程序错误** *XXX*指出了这些错误，其中*XXX*是 i/o 错误代码。

在故障转储文件中，消息**错误检查0xC9 （驱动程序\_验证程序\_IOMANAGER\_冲突）** 以及 i/o 错误代码将记录这些错误。 在这种情况下，i/o 错误代码将显示为 bug 检查0xC9 的第一个参数。

在内核调试器（KD 或 WinDbg）中，消息**WDM 驱动程序错误**和描述性文本字符串记录了这些错误。 当内核调试器处于活动状态时，可以忽略第2级错误并恢复系统操作。 （这不能与任何其他 bug 检查一起进行。）

蓝屏、故障转储文件和内核调试器也会显示附加信息。 有关所有 i/o 验证级别2错误消息的完整说明，请参阅[**Bug 检查 0xC9**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc9--driver-verifier-iomanager-violation)。

### <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项

您可以使用驱动程序验证器管理器或 Verifier 命令行为一个或多个驱动程序激活增强的 i/o 验证功能。 有关详细信息，请参阅[选择驱动程序验证程序选项](selecting-driver-verifier-options.md)。

**请注意**，在 windows 7 和更高版本的 Windows 操作系统中  ，当你选择 " [i/o 验证](i-o-verification.md)" 时，将自动激活增强的 i/o 验证。 不能将其选择为单独的选项。

 

-   **在命令行中**

    在命令行中，增强的 i/o 验证选项由**Bit 6 （0x40）** 表示。 若要激活增强型 i/o 验证，请使用0x40 的标志值或将0x40 添加到标志值。 例如：

    ```
    verifier /flags 0x40 /driver MyDriver.sys
    ```

    此功能将在下一次启动后处于活动状态。

    在 Windows Vista 和更高版本的 Windows 上，还可以通过将 **/volatile**参数添加到命令来激活和停用增强的 i/o 验证，而无需重新启动计算机。 例如：

    ```
    verifier /volatile /flags 0x40 /adddriver MyDriver.sys
    ```

    此设置将立即生效，但当你关闭或重新启动计算机时，此设置会丢失。 有关详细信息，请参阅[使用可变设置](using-volatile-settings.md)。

-   **使用驱动程序验证器管理器**

    1.  启动驱动程序验证器管理器。 在命令提示符窗口中键入**Verifier** 。
    2.  选择 "**创建自定义设置（对于代码开发人员）** "，然后单击 "**下一步**"。
    3.  选择 "**从完整列表中选择单个设置**"。
    4.  选择（检查）**增强的 i/o 验证**。

    "DMA 验证" 功能也包含在标准设置中。 若要使用此功能，请在驱动程序验证器管理器中单击 "**创建标准设置**"。

 

 





