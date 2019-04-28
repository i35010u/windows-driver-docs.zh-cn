---
title: 增强的 I/O 验证
description: 增强的 I/O 验证
ms.assetid: ce8a0b22-fa27-45e5-b013-b3accf604ed4
keywords:
- 增强的 I/O 验证功能 WDK Driver Verifier
- I/O 验证功能 WDK Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2edd9c7ed87e3e9a029c44ae335b02e116d90c80
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344852"
---
# <a name="enhanced-io-verification"></a>增强的 I/O 验证


此功能是仅在 Windows XP 和更高版本的 Windows 操作系统中可用。

在 Windows 7 和更高版本的 Windows 操作系统中，当您选择的 I/O 验证时，将自动激活增强的 I/O 验证。 它不可用或有必要以选择它作为单独的选项。

增强的 I/O 验证激活时，驱动程序验证程序监视多个 I/O 管理器例程的调用并执行压力测试的 PnP Irp、 power Irp 和 WMI Irp。

增强的 I/O 验证独立于在 Windows Vista 和 Windows XP 中，将激活[I/O 验证](i-o-verification.md)，但选择这两个选项提供对于 I/O 在驱动程序的接口方法的更完整测试。

### <a name="span-idfeaturesofenhancedioverificationspanspan-idfeaturesofenhancedioverificationspanfeatures-of-enhanced-io-verification"></a><span id="features_of_enhanced_i_o_verification"></span><span id="FEATURES_OF_ENHANCED_I_O_VERIFICATION"></span>增强的 I/O 验证的功能

激活增强的 I/O 验证时，驱动程序验证程序将添加以下检查。

-   监视以确保该驱动程序返回状态的所有 Irp\_PENDING 当且仅当它被称为[ **IoMarkIrpPending**](https://msdn.microsoft.com/library/windows/hardware/ff549422)。

-   监视使用[ **IoDeleteDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff549083)若要验证的驱动程序不会删除同一设备的更多一次，并检测不适当的分离和删除的设备对象。

-   验证该驱动程序正确展开所有[ **IoSkipCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550355)调用。

新的压力和测试包括：

-   在混合的顺序枚举设备，以确保插即用 (PnP) 驱动程序不做出假设设备启动顺序。

-   调整的即插即用的状态和电源 Irp，在它们完成后，若要找出那些已从其调度例程返回不正确的状态。

-   发送伪造 Power Irp 要测试其驱动程序代码路径的问题。

-   发送伪造 WMI Irp 要测试其驱动程序代码路径的问题。

-   每个 WDM 堆栈中插入伪造的筛选器。

### <a name="span-iddisplayingenhancedioverificationerrorsspanspan-iddisplayingenhancedioverificationerrorsspandisplaying-enhanced-io-verification-errors"></a><span id="displaying_enhanced_i_o_verification_errors"></span><span id="DISPLAYING_ENHANCED_I_O_VERIFICATION_ERRORS"></span>显示增强的 I/O 验证错误

通过增强的 I/O 验证捕获到的驱动程序错误都显示在与那些由捕获相同的方式[级别 2 的 I/O 验证](i-o-verification.md)。

在蓝色屏幕上，这些错误进行说明的消息**IO 系统验证错误**和字符串**WDM 驱动程序错误** *XXX*，其中*XXX*是 I/O 错误代码。

在崩溃转储文件中，这些错误进行说明的消息**检测错误 0xC9 (驱动程序\_VERIFIER\_IOMANAGER\_冲突)**，以及 I/O 错误代码。 在这种情况下，I/O 错误代码显示为 bug 检查 0xC9 的第一个参数。

在内核调试器 （KD 或 WinDbg） 中，这些错误记录的消息**WDM 驱动程序错误**和说明性文本字符串。 当内核调试程序处于活动状态时，则可以忽略第 2 级错误并继续执行系统操作。 （这是不可能与任何其他 bug 检查。）

蓝色的屏幕、 故障转储文件和内核调试程序每个显示其他信息。 所有 I/O 验证级别 2 的错误消息的完整说明，请参阅[ **Bug 检查 0xC9**](https://msdn.microsoft.com/library/windows/hardware/ff560205)。

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项

可以使用驱动程序验证程序管理器或 Verifier.exe 命令行来激活一个或多个驱动程序的增强的 I/O 验证功能。 有关详细信息，请参阅[选择 Driver Verifier 选项](selecting-driver-verifier-options.md)。

**请注意**  在 Windows 7 和更高版本的 Windows 操作系统中，增强的 I/O 验证将自动激活选择时[I/O 验证](i-o-verification.md)。 它不可用或有必要以选择它作为单独的选项。

 

-   **在命令行**

    在命令行中，由表示增强的 I/O 验证选项**位 6 (0x40)**。 若要激活增强的 I/O 验证，使用 0x40 标志值，或将 0x40 添加到标志值。 例如：

    ```
    verifier /flags 0x40 /driver MyDriver.sys
    ```

    在下一次启动后，该功能将处于活动状态。

    在 Windows Vista 和更高版本的 Windows 上，您可以还激活和停增强的 I/O 验证用而无需重启计算机，通过添加 **/volatile**命令参数。 例如：

    ```
    verifier /volatile /flags 0x40 /adddriver MyDriver.sys
    ```

    此设置将立即生效，但当你关闭或重新启动计算机时将丢失。 有关详细信息，请参阅[使用易失性设置](using-volatile-settings.md)。

-   **使用驱动程序验证程序管理器**

    1.  启动驱动程序验证器管理器。 类型**Verifier**在命令提示符窗口中。
    2.  选择**创建自定义设置 （适用于代码开发人员）** ，然后单击**下一步**。
    3.  选择**从完整的列表中选择单个设置**。
    4.  选择 （选中）**增强的 I/O 验证**。

    DMA 验证功能也包含在标准设置。 若要使用此功能，驱动程序验证程序管理器中，单击**创建标准设置**。

 

 





