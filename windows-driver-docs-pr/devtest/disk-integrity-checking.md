---
title: 磁盘完整性检查
description: 磁盘完整性检查
keywords:
- 磁盘完整性检查功能 WDK 驱动程序验证程序
- 磁盘存储准确性 WDK 驱动程序验证程序
- 存储准确性 WDK 驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89c42aab48b19d4f5d8e8d49849f1c29252e9f31
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839023"
---
# <a name="disk-integrity-checking"></a>磁盘完整性检查


## <span id="ddk_disk_integrity_verification_tools"></span><span id="DDK_DISK_INTEGRITY_VERIFICATION_TOOLS"></span>


驱动程序验证程序的磁盘完整性检查功能可监视所有硬盘访问，以确定磁盘是否准确存储信息。 如果磁盘上的数据显示为 "已更改"，则会发出 bug 检查。

此驱动程序验证程序选项是在 Windows Server 2003 中引入的，并且已作为一个从 Windows 7 开始的选项删除。

### <a name="span-idhow_disk_integrity_checking_worksspanspan-idhow_disk_integrity_checking_worksspanhow-disk-integrity-checking-works"></a><span id="how_disk_integrity_checking_works"></span><span id="HOW_DISK_INTEGRITY_CHECKING_WORKS"></span>磁盘完整性检查的工作原理

激活磁盘完整性检查时，可以选择验证附加到计算机的所有物理磁盘。

一旦 Windows 及其驱动程序加载完成，驱动程序验证程序就会开始监视对这些驱动器执行的所有读取和写入操作。 驱动程序验证程序为每个访问的扇区计算 CRC (循环冗余检查) 校验和，并保存此值。 下一次访问此扇区时，驱动程序验证器会重新计算此校验和，并将其与以前的值进行比较。

如果校验和值发生更改，则表示磁盘完整性出现问题--读取操作返回错误的信息，或磁盘媒体自上次访问后已更改其内容。 发生这种情况时，驱动程序验证程序会发出 bug 检查0xC4，并将参数1等于0xA0。 其他参数用于标识发出请求的 IRP、较低设备的设备对象以及发生错误的扇区。 有关详细信息，请参阅 [**Bug 检查 0xC4**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (DRIVER \_ VERIFIER \_ 检测到 \_ 违规) 。

### <a name="span-idperformance_issuesspanspan-idperformance_issuesspanperformance-issues"></a><span id="performance_issues"></span><span id="PERFORMANCE_ISSUES"></span>性能问题

磁盘完整性检查功能使硬盘访问 perceptibly 速度更慢。 如果计算机 RAM 不足，这种性能降低会更重要。 使用磁盘完整性检查来调查磁盘问题，但在每次运行驱动程序验证程序以测试驱动程序时，不激活。

**注意**   磁盘完整性检查功能不适合在使用群集共享磁盘的系统上工作。 如果在此类系统上启用磁盘完整性检查功能，则磁盘完整性检查可能会导致 bug 检查出错。 因此，强烈建议您不要在具有群集共享磁盘的系统上启用此功能。
此外，在某些情况下，可能会导致对具有非群集磁盘的系统进行错误检查。 这些情况包括：

-   内存写入缓冲区写入缓冲区

-   并发入和写入同一扇区

 

### <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项

您可以通过使用驱动程序验证程序管理器或 Verifier.exe 命令行来激活磁盘完整性检查选项。 驱动程序验证器管理器使你能够确定验证了哪些磁盘。 如果使用命令行，将验证所有磁盘。 有关详细信息，请参阅 [选择驱动程序验证程序选项](selecting-driver-verifier-options.md)。

-   **在命令行中**

    在命令行中，磁盘完整性检查选项由 **/disk** 参数表示。 例如：

    ```
    verifier /disk /driver MyDriver.sys
    ```

    此功能将在下一次启动后处于活动状态。 如果不在任何 Windows 版本上重新启动计算机，则无法激活磁盘完整性检查选项。

-   **使用驱动程序验证器管理器**
    1.  选择 " **为代码开发人员 (创建自定义设置")** ，然后单击 " **下一步**"。
    2.  选择 " **从完整列表中选择单个设置**"。
    3.  选择 (检查) **磁盘完整性检查**。

 

