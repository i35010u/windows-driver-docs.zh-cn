---
title: Bug 检查 0x7B INACCESSIBLE_BOOT_DEVICE
description: INACCESSIBLE_BOOT_DEVICE bug 检查具有 0x0000007B 值。 此 bug 检查指示 Microsoft Windows 操作系统将无法在启动期间的对系统分区的访问。
ms.assetid: 0dfcb519-4ea3-4419-a1c3-60fdff96404d
keywords:
- Bug 检查 0x7B INACCESSIBLE_BOOT_DEVICE
- INACCESSIBLE_BOOT_DEVICE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INACCESSIBLE_BOOT_DEVICE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9d560f7216de76fea185bd7e5e679d79ae128112
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239634"
---
# <a name="bug-check-0x7b-inaccessiblebootdevice"></a>Bug 检查 0x7B：无法访问\_启动\_设备


无法访问\_启动\_设备错误检查的值为 0x0000007B。 此 bug 检查指示 Microsoft Windows 操作系统将无法在启动期间的对系统分区的访问。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="inaccessiblebootdevice-parameters"></a>无法访问\_启动\_设备参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>UNICODE_STRING 结构的地址或无法安装的设备对象的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

若要确定参数 1 的含义，查看它指向的数据。 如果在此地址的第一个单词 (USHORT) 为偶数，则参数 1 是 Unicode 字符串的开头。 如果在此地址的第一个单词 (USHORT)，0x3 参数 1 是一个设备对象的第一个字段 （类型）。

-   如果此参数指向一个设备对象，应读取的启动设备在文件系统初始化失败，或只是无法识别数据的启动设备上为文件系统结构。 在此情况下，指定的设备对象是无法装入的对象。

-   如果此参数指向的 Unicode 字符串，您必须读取此地址处的第一个 8 字节。 这两个字节构成 UNICODE\_字符串结构，定义如下：

    ```cpp
    USHORT Length;
    USHORT MaximumLength;
    PWSTR Buffer;
    ```

    **长度**字段用于提供字符串的实际长度。 **缓冲区**字段指向字符串的开头 (**缓冲区**是始终保持至少 0x80000000。)

    实际的字符串包含从正在尝试启动的设备的高级 RISC 计算 (ARC) 规范名称。 弧线名称是用于标识弧线环境中的设备的通用方法。

<a name="cause"></a>原因
-----

无法访问\_启动\_设备 bug 检查通常会出现由于启动设备故障。 在 I/O 系统初始化期间启动设备驱动程序可能无法初始化启动设备 （通常硬盘）。

文件系统初始化可能已失败，因为它无法识别数据上的启动设备。 此外，重新分区系统分区、 更改 BIOS 配置或安装磁盘控制器可能会引发此错误。

由于不兼容磁盘硬件，也可以发生此错误。 如果系统的初始安装时出错，系统可能安装了不受支持的磁盘控制器上。 某些磁盘控制器需要其他驱动程序，Windows 启动时必须存在。

<a name="resolution"></a>分辨率
----------

在系统启动时，始终会发生此错误。 此错误通常会出现才能建立连接调试器，因此很难调试。 此外，操作系统可能无法访问，错误日志可能为空，因为操作系统已不启动到足够小以启动这些子系统。

**\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\\***

**如果您不能启动 Windows**

**\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\\***

如果您收到此停止代码，而 Windows 不会向前引导到操作系统，请尝试以下解决方法：

**还原任何最新的硬件更改**

删除任何最近添加的硬件，尤其是硬盘驱动器或控制器，以查看错误是否得到解决。 如果有问题的硬件，硬盘驱动器上的磁盘固件版本可能与你的 Windows 操作系统版本不兼容。 更新，请与制造商联系。 如果删除另一个硬件，则在解决可能存在 IRQ 或 I/O 端口冲突。 重新配置新设备根据制造商的说明。

如果你最近已更改 BIOS 设置，例如从旧的控制器模式更改为在 BIOS 中 AHCI 还原这些更改。 有关详细信息，请参阅 <https://en.wikipedia.org/wiki/Advanced_Host_Controller_Interface>

**存储设备兼容性检查**

确认所有硬盘驱动程序、 硬盘控制器和任何其他存储适配器是与安装的 Windows 版本兼容。 例如，可以获取有关在兼容性信息[Windows 10 规范](https://www.microsoft.com/windows/windows-10-specifications)。

**更新 BIOS 和固件**

检查系统 BIOS 和存储控制器固件更新的可用性。

**使用媒体创建工具来创建可启动 U 盘或 DVD**

使用媒体创建工具，使用另一台计算机创建可启动 USB 闪存驱动器或 DVD。 使用它来执行全新安装，单击安装程序文件或从 USB 启动。

有关详细信息，请参阅[获取 Windows 10](https://www.microsoft.com/software-download/windows10)。

请注意，可能需要禁用功能，例如快速 BIOS 启动，或者你可能不会能够访问启动设备优先级菜单。 更改要从 FDD (FlashDiskDrive) 或而不是 HDD DVD 启动的 BIOS 菜单在您启动序列优先级。

**常见的启动菜单键**

每个制造商生产的启动菜单键而异，通常使用这些密钥。 检查系统文档以确定使用何种启动密钥。

F12 ESC F9 F10 F8**常见 BIOS 设置密钥**

每个制造商生产的 BIOS 设置参数而异，通常使用这些密钥。 检查系统文档以确定使用何种安装程序密钥。

ESC DEL F2 **\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\\***

**如果可以启动 Windows**

**\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\\***

-   **启动至安全模式和正常启动**

    完成以下步骤来启动进入安全模式。 启动进入安全模式下加载一组核心可能会允许再一次访问的存储系统的存储驱动程序。

    若要进入安全模式下，使用**更新和安全**设置中。 选择**恢复**-&gt;**高级启动**启动到维护模式。 在生成菜单中选择**进行故障排除**- &gt; **高级选项** - &gt; **启动设置** - &gt; **重新启动**。 Windows 重新启动到后**启动设置**屏幕上，选择选项 4、 5 或 6 到安全模式下启动。

    Windows 加载后在安全模式下，重新启动 PC 以查看是否将加载相应的存储驱动程序和存储设备被识别。

    安全模式还可通过按功能键上启动，例如 F8。 从特定的启动选项的系统制造商参考信息。

-   使用扫描磁盘实用程序以确认没有任何文件系统错误。 右键单击你想要扫描，并选择在驱动器上**属性**。 单击**工具**。 单击**立即检查**按钮。
-   运行病毒检测程序。 病毒可能会感染所有类型的 for Windows，格式化的硬盘，并生成磁盘损坏可生成系统 bug 检查代码。 请确保病毒检测程序会检查存在感染主启动记录。

-   对于 IDE 设备定义上的 IDE 端口作为主仅。 此外检查了正确的每个 IDE 设备**母版/从属/独立**设置。 请尝试删除除硬盘以外的所有 IDE 设备。 最后，检查事件查看器中的系统日志可能有助于识别设备或导致错误的驱动程序的其他错误消息。

-   确认在硬盘上没有足够的可用空间。 操作系统和某些应用程序需要足够的可用空间来创建交换文件和其他功能。 根据系统配置，具体要求各不相同，但它通常是最好有可用的 10%到 15%可用空间。

-   查找范围**设备管理器**若要查看的任何设备都带有感叹号 （！）。 查看任何错误的驱动程序的驱动程序属性中显示的事件日志。 请尝试更新相关的驱动程序。

-   检查事件查看器中的系统日志可能会帮助找出设备或导致错误的驱动程序的其他错误消息。 有关详细信息，请参阅[打开事件查看器](https://windows.microsoft.com/windows/what-information-event-logs-event-viewer#1TC=windows-7)。 查找为蓝色的屏幕的同一时间范围内发生在系统日志中的关键错误。

-   您可以尝试运行硬件诊断程序提供的系统制造商。

-   使用系统文件检查器工具来修复丢失或损坏系统文件。 系统文件检查器是一个实用程序允许用户在 Windows 系统文件损坏扫描和还原 Windows 中的损坏的文件。 使用以下命令运行系统文件检查器 (SFC.exe)。

    ```console
    SFC /scannow
    ```

    有关详细信息，请参阅[使用的系统文件检查器工具来修复丢失或损坏系统文件](https://support.microsoft.com/kb/929833)。

-   后自动修复，在选择选项屏幕上，选择**进行故障排除&gt;高级选项&gt;系统还原**。 此选项将你的电脑带回到较早的时间点（称为系统还原点）。 还原点时安装新的应用程序、 驱动程序、 更新或手动创建还原点时生成。 遇到错误之前，请选择一个还原点。

-   使用内核调试程序附加到系统，并进一步分析失败，如备注中所述。

<a name="remarks"></a>备注
-------

**调查存储系统配置**

很多达深入地了解 Windows 安装的启动设备。 例如，你可以调查以下各项：

-   找出哪些类型的控制器启动设备连接到 （SATA、 IDE 等）。 如果可以启动系统，可以使用设备管理器检查控制器和磁盘驱动程序属性，并查看关联的驱动程序文件以及错误事件。

-   指示是否其他设备则附加到同一个控制器上 （SSD、 DVD，等） 的启动设备。

-   请注意使用通常 NTFS 驱动器的文件系统。

**若要分析此使用内核调试程序时出错：** 运行[ **lm （列表加载模块）** ](lm--list-loaded-modules-.md)命令以查看哪些模块加载尝试隔离特定的驱动程序在调试器中。 验证已加载以下驱动程序。

*磁盘*

```dbgcmd
           
0: kd> lm m disk
Browse full module list
start             end                 module name
fffff806`bd0b0000 fffff806`bd0cd000   disk       (deferred)
```

*partmgr*

```dbgcmd
0: kd> lm m partmgr
Browse full module list
start             end                 module name
fffff806`bc5a0000 fffff806`bc5c1000   partmgr    (deferred)
```

*NTFS*

```dbgcmd
0: kd> lm m ntfs
Browse full module list
start             end                 module name
fffff806`bd3f0000 fffff806`bd607000   NTFS       (deferred)
```

*classpnp*

```dbgcmd
 0: kd> lm m classpnp
Browse full module list
start             end                 module name
fffff806`bd0d0000 fffff806`bd131000   CLASSPNP   (deferred)
```

*pci*

```dbgcmd
0: kd> lm m pci
Browse full module list
start             end                 module name
fffff806`bc440000 fffff806`bc494000   pci        (deferred) 
```

此外请确保控制器驱动程序已加载。 例如对于 SATA RAID 控制器，这可能是*iaStorA.Sys*驱动程序，或它可能是*EhStorClass*驱动程序。

```dbgcmd
0: kd> lm m EhStorClass
Browse full module list
start             end                 module name
fffff806`bcbb0000 fffff806`bcbcb000   EhStorClass   (deferred) 
```

列出包含"存储"，storahci，可能存在的驱动程序。

```dbgcmd
0: kd> lm m stor*
Browse full module list
start             end                 module name
fffff806`bcb00000 fffff806`bcb23000   storahci   (deferred)             
fffff806`bcb30000 fffff806`bcbaa000   storport   (deferred)             
fffff806`c0770000 fffff806`c0788000   storqosflt   (deferred)
```

**带有附加调试程序启动**

如果可以连接在调试器中启动目标系统，则发出[ **！ devnode 0 1** ](-devnode.md)检测的错误发生时。 您将看到哪些设备缺少驱动程序或无法启动，且未启动的原因可能是明显。

一个原因可能是该即插即用和播放不能将资源分配给的启动设备。 可以通过为服务中查找项来验证此限制。 如果状态标志包括 DNF\_不足\_资源或不包括 DNF\_启动或 DNF\_枚举，可能会找到问题。 请尝试 **！ devnode 0 1 storahci**节省一些时间，而不是转储整个设备树。

```dbgcmd
0: kd> !devnode 0 1 storahci
Dumping IopRootDeviceNode (= 0xffffb9053d94d850)
DevNode 0xffffb9053e8dea50 for PDO 0xffffb9053e8da060
  InstancePath is "PCI\VEN_8086&DEV_3B22&SUBSYS_304A103C&REV_05\3&21436425&0&FA"
  ServiceName is "storahci"
  State = DeviceNodeStarted (0x308)
  Previous State = DeviceNodeEnumerateCompletion (0x30d)
  DevNode 0xffffb9053e88db30 for PDO 0xffffb9053e890060
    InstancePath is "SCSI\Disk&Ven_&Prod_ST3500418AS\4&23d99fa2&0&000000"
    ServiceName is "disk"
    State = DeviceNodeStarted (0x308)
    Previous State = DeviceNodeEnumerateCompletion (0x30d)
  DevNode 0xffffb9053e88d850 for PDO 0xffffb9053e88e060
    InstancePath is "SCSI\CdRom&Ven_hp&Prod_DVD-RAM_GH60L\4&23d99fa2&0&010000"
    ServiceName is "cdrom"
    TargetDeviceNotify List - f 0xffffdf0ae9bbb0e0  b 0xffffdf0aea874710
    State = DeviceNodeStarted (0x308)
    Previous State = DeviceNodeEnumerateCompletion (0x30d)
```

 

 




