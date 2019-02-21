---
title: 磁盘完整性检查
description: 磁盘完整性检查
ms.assetid: bb838594-637c-4fc4-b2ec-964b69faabcf
keywords:
- 磁盘完整性检查功能 WDK Driver Verifier
- 磁盘存储准确性 WDK Driver Verifier
- 存储准确性 WDK Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19f7a4deb4a694ff39be7d0d2b694e9a1aad8dea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554421"
---
# <a name="disk-integrity-checking"></a>磁盘完整性检查


## <span id="ddk_disk_integrity_verification_tools"></span><span id="DDK_DISK_INTEGRITY_VERIFICATION_TOOLS"></span>


驱动程序验证程序的磁盘完整性检查功能监视所有硬盘磁盘访问，以确定磁盘是否准确地存储信息。 如果磁盘上的数据将显示更改，则会发出错误检查。

此驱动程序验证程序选项在 Windows Server 2003 中引入，并已删除作为选项从 Windows 7 开始。

### <a name="span-idhowdiskintegritycheckingworksspanspan-idhowdiskintegritycheckingworksspanhow-disk-integrity-checking-works"></a><span id="how_disk_integrity_checking_works"></span><span id="HOW_DISK_INTEGRITY_CHECKING_WORKS"></span>磁盘完整性检查的工作原理

激活时磁盘完整性检查，您可以选择验证任何或所有附加到您的计算机的物理磁盘。

一旦加载 Windows，其驱动程序，驱动程序验证程序开始监视所有读取和写入到这些驱动器所做的操作。 驱动程序验证程序计算每个扇区的访问，并将保存此值的 CRC （循环冗余检查） 校验和值。 下次访问此扇区时，驱动程序验证程序重新计算此校验和，并将它与以前的值进行比较。

如果校验和值发生更改，则表明磁盘完整性问题--读取的操作返回有故障的信息或磁盘介质的上次访问以来已更改其内容。 在此情况下，驱动程序验证程序问题 bug 检查与参数 1 等于 0xA0 0xC4。 其他参数标识 IRP 发出请求，较低的设备，并出现错误的扇区的设备对象。 有关详细信息，请参阅[ **Bug 检查 0xC4** ](https://msdn.microsoft.com/library/windows/hardware/ff560187) (驱动程序\_VERIFIER\_检测到\_冲突)。

### <a name="span-idperformanceissuesspanspan-idperformanceissuesspanperformance-issues"></a><span id="performance_issues"></span><span id="PERFORMANCE_ISSUES"></span>性能问题

磁盘完整性检查功能可使硬盘访问 perceptibly 速度较慢。 如果在计算机上 RAM 不足时，此性能下降是更大。 使用磁盘完整性检查，调查磁盘问题，但未激活时运行驱动程序验证程序来测试驱动程序时。

**请注意**  磁盘完整性检查功能没有设计成可使用群集共享的磁盘的系统上。 如果启用此类系统上的磁盘完整性检查功能时，磁盘完整性检查可能会错误地导致出现的 bug 检查。 因此，强烈建议不启用此功能在具有群集共享磁盘的系统上。
此外，有 false 错误检查的具有非群集磁盘的系统上可能会导致某些情况。 这些情况包括：

-   内存将写入到传输的数据写入缓冲区

-   正在进行的并发读取和写入到同一区域

 

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项

可以使用驱动程序验证程序管理器或 Verifier.exe 命令行来激活磁盘完整性检查选项。 驱动程序验证程序管理器可以确定哪些磁盘进行验证。 如果使用命令行时，会验证所有磁盘。 有关详细信息，请参阅[选择 Driver Verifier 选项](selecting-driver-verifier-options.md)。

-   **在命令行**

    在命令行中，磁盘完整性检查选项由 **/磁盘**参数。 例如：

    ```
    verifier /disk /driver MyDriver.sys
    ```

    在下一次启动后，该功能将处于活动状态。 您不能不重启的计算机上任何版本的 Windows 激活磁盘完整性检查选项。

-   **使用驱动程序验证程序管理器**
    1.  选择**创建自定义设置 （适用于代码开发人员）** ，然后单击**下一步**。
    2.  选择**从完整的列表中选择单个设置**。
    3.  选择 （选中）**磁盘完整性检查**。

 

 





