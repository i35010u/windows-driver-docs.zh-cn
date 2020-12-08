---
title: Bug 检查 0x7B INACCESSIBLE_BOOT_DEVICE
description: INACCESSIBLE_BOOT_DEVICE bug 检查的值为0x0000007B。 此错误检查表示在启动过程中，Microsoft Windows 操作系统已失去对系统分区的访问权限。
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
ms.openlocfilehash: b00036189d8e91fa838814df868a9a93ffe3682d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819264"
---
# <a name="bug-check-0x7b-inaccessible_boot_device"></a>Bug 检查0x7B：无法访问的 \_ 启动 \_ 设备


不可访问的 \_ 启动 \_ 设备错误检查的值为0x0000007b。 此错误检查表示在启动过程中，Microsoft Windows 操作系统已失去对系统分区的访问权限。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="inaccessible_boot_device-parameters"></a>无法访问的 \_ 启动 \_ 设备参数


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
<td align="left"><p>UNICODE_STRING 结构的地址，或者无法装载的设备对象的地址</p></td>
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

 

若要确定参数1的含义，请查看它所指向的数据。 如果此地址的第一个单词 (USHORT) 为偶数，则参数1是 Unicode 字符串的开头。 如果此地址中的第一个单词 (USHORT) 为0x3，则参数1是设备对象) 的第一个字段 (类型。

-   如果此参数指向某个设备对象，则该文件系统将无法初始化，或者只是无法将启动设备上的数据识别为文件系统结构。 在这种情况下，指定的设备对象是无法装载的对象。

-   如果此参数指向 Unicode 字符串，则必须读取此地址的前8个字节。 这些字节构成 UNICODE \_ 字符串结构，定义如下：

    ```cpp
    USHORT Length;
    USHORT MaximumLength;
    PWSTR Buffer;
    ```

    " **长度** " 字段提供字符串的实际长度。 **缓冲区** 字段指向字符串的开头 (**缓冲区** 始终至少是0x80000000。 ) 

    实际字符串包含从尝试启动的设备的高级 RISC 计算 (ARC) 规范名称。 ARC 名称是在弧形环境中标识设备的一种通用方法。

<a name="cause"></a>原因
-----

\_ \_ 由于启动设备故障，因此经常发生不可访问的启动设备错误检查。 在 i/o 系统初始化期间，启动设备驱动程序可能无法初始化启动设备， (通常是硬盘) 。

文件系统初始化可能已失败，因为它无法识别启动设备上的数据。 此外，重新分区系统分区、更改 BIOS 配置或安装磁盘控制器可能会导致此错误。

此错误还可能是由于磁盘硬件不兼容引起的。 如果错误发生在系统初始安装时，则系统可能已安装在不受支持的磁盘控制器上。 在 Windows 启动时，某些磁盘控制器需要提供其他驱动程序。

<a name="resolution"></a>解决方法
----------

系统启动时，始终会出现此错误。 此错误经常在建立调试器连接之前发生，因此调试可能会很困难。 此外，操作系统可能无法访问，并且错误日志可能为空，因为 OS 尚未启动就足以启动这些子系统。

**\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\\***

**如果无法启动 Windows**

**\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\\***

如果收到此 stop 代码，但 Windows 不会继续进入操作系统，请尝试以下操作：

**还原任何最近的硬件更改**

删除最近添加的任何硬件（特别是硬盘驱动器或控制器），以查看是否已解决错误。 如果有问题的硬件是硬盘驱动器，则磁盘固件版本可能与你的 Windows 操作系统版本不兼容。 请联系制造商以获取更新。 如果删除了另一块硬件并且错误已解决，则可能存在 IRQ 或 i/o 端口冲突。 根据制造商的说明重新配置新设备。

如果最近更改了 BIOS 设置，例如在 BIOS 中将控制器模式从旧版本更改为 AHCI，请还原这些更改。 有关详细信息，请参阅<https://en.wikipedia.org/wiki/Advanced_Host_Controller_Interface>。

**检查存储设备的兼容性**

确认所有硬盘驱动程序、硬盘控制器和任何其他存储适配器都与安装的 Windows 版本兼容。 例如，你可以在 [Windows 10 规范](https://www.microsoft.com/windows/windows-10-specifications)中获取有关兼容性的信息。

**更新 BIOS 和固件**

检查系统 BIOS 和存储控制器固件更新的可用性。

**使用媒体创建工具创建可启动的 USB 拇指驱动器或 DVD**

使用其他计算机创建可启动的 USB 拇指驱动器或 DVD，使用媒体创建工具。 通过选择安装程序文件或从 USB 启动，可以使用它来执行全新安装。

有关详细信息，请参阅 [获取 Windows 10](https://www.microsoft.com/software-download/windows10)。

请注意，您可能需要禁用一些功能，如快速 BIOS 启动，或者您可能无法访问 "启动设备优先级" 菜单。 在 BIOS 菜单中更改启动顺序优先级，以便从 FDD (FlashDiskDrive) 或 DVD （而不是 HDD）启动。

**常见启动菜单键**

启动菜单密钥因制造商而异，通常使用这些密钥。 查看系统文档，确定所使用的启动密钥。

F12 ESC F9 （**常见 BIOS 设置密钥**）

BIOS 设置密钥因制造商而异，通常使用这些密钥。 查看系统文档，确定所使用的设置密钥。

ESC DEL F2 **\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\\***

**如果可以启动 Windows**

**\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\\***

-   **启动到安全模式，然后正常启动**

    完成以下步骤以启动到安全模式。 启动到安全模式时，将加载一组核心存储驱动程序，这些驱动程序可能允许再次访问存储系统。

    若要进入安全模式，请使用 "设置" 中的 " **更新和安全** "。 选择 "**恢复** - &gt; **高级启动**" 以启动到维护模式。 在出现的菜单中，**选择 "** - &gt; **高级选项**" "启动  - &gt; **设置**  - &gt; **重新启动**"。 Windows 重启到 " **启动设置** " 屏幕后，选择 "选项"、"4"、"5" 或 "6" 以启动到安全模式。

    在安全模式下加载 Windows 后，请重新启动计算机，查看是否将加载适当的存储驱动程序以及是否可识别存储设备。

    安全模式也可通过在启动时按功能键来提供，例如 F8。 请参阅系统制造商提供的有关特定启动选项的信息。

-   使用扫描磁盘实用工具确认没有文件系统错误。 选择并按住 (或右键单击要扫描的驱动器) ，然后选择 " **属性**"。 选择 " **工具**"。 选择 " **立即检查** " 按钮。
-   运行病毒检测程序。 病毒可能会感染为 Windows 格式化的所有类型的硬盘，导致磁盘损坏可能生成系统 bug 检查代码。 请确保病毒检测程序检查主启动记录中是否有病毒感染。

-   对于 IDE 设备，请将板载 IDE 端口定义为 "仅主要"。 还要检查每个 IDE 设备是否有正确的 **主/从/独立** 设置。 尝试删除除硬盘之外的所有 IDE 设备。 最后，检查中的系统日志事件查看器是否有可能有助于识别导致错误的设备或驱动程序的其他错误消息。

-   确认硬盘上有足够的可用空间。 操作系统和某些应用程序需要足够的可用空间来创建交换文件和其他功能。 根据系统配置，具体要求会有所不同，但通常最好使用10% 到15% 的可用空间。

-   查看 **设备管理器** 查看是否有任何设备标记为惊叹号 (！ ) 。 查看在驱动程序属性中显示的任何错误驱动程序的事件日志。 请尝试更新相关驱动程序。

-   检查中的系统日志事件查看器是否有其他错误消息，这些错误消息可能有助于找出导致错误的设备或驱动程序。 有关详细信息，请参阅[打开事件查看器](https://support.microsoft.com/hub/4338813/windows-help#1TC=windows-7)。 在系统日志中查找与蓝屏同时出现的严重错误。

-   你可以尝试运行系统制造商提供的硬件诊断。

-   使用系统文件检查器工具修复丢失或损坏的系统文件。 系统文件检查器是 Windows 中的一个实用工具，它允许用户在 Windows 系统文件中扫描损坏并还原损坏的文件。 使用以下命令 ( # A0) 运行系统文件检查器工具。

    ```console
    SFC /scannow
    ```

    有关详细信息，请参阅 [使用系统文件检查器工具修复丢失或损坏的系统文件](https://support.microsoft.com/help/929833/use-the-system-file-checker-tool-to-repair-missing-or-corrupted-system)。

-   自动修复后，在 "选择选项" 屏幕上，选择 " **&gt; 高级选项" " &gt; 系统还原疑难解答**"。 此选项会将你的电脑恢复到以前的时间点，称为系统还原点。 当你安装新的应用程序、驱动程序、更新或手动创建还原点时，将生成还原点。 出现错误之前，请选择一个还原点。

-   使用内核调试器附加到系统，并进一步分析故障，如 "备注" 中所述。

<a name="remarks"></a>备注
-------

**调查存储系统配置**

了解有关安装 Windows 的引导设备的尽可能多的信息非常有用。 例如，可以调查以下各项：

-   了解启动设备连接到 (SATA、IDE 等) 的控制器的类型。 如果可以启动系统，你可以使用设备管理器来检查控制器和磁盘驱动程序的属性，并查看关联的驱动程序文件以及错误事件。

-   指示是否将其他设备连接到启动设备位于 (SSD、DVD 等) 上的控制器。

-   记下在驱动器上使用的文件系统，通常为 NTFS。

**若要使用内核调试器分析此错误：** 在调试程序中运行 [**lm (List)**](lm--list-loaded-modules-.md) 命令，以查看加载哪些模块来尝试隔离特定驱动程序。 验证是否已加载以下驱动程序。

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

*pci-e*

```dbgcmd
0: kd> lm m pci
Browse full module list
start             end                 module name
fffff806`bc440000 fffff806`bc494000   pci        (deferred) 
```

此外，请确保已加载控制器驱动程序。 例如，对于 SATA RAID 控制器，这可能是 *iaStorA.Sys* 驱动程序，也可能是 *EhStorClass* 驱动程序。

```dbgcmd
0: kd> lm m EhStorClass
Browse full module list
start             end                 module name
fffff806`bcbb0000 fffff806`bcbcb000   EhStorClass   (deferred) 
```

列出了包含 "stor" （storahci）的驱动程序可能存在。

```dbgcmd
0: kd> lm m stor*
Browse full module list
start             end                 module name
fffff806`bcb00000 fffff806`bcb23000   storahci   (deferred)             
fffff806`bcb30000 fffff806`bcbaa000   storport   (deferred)             
fffff806`c0770000 fffff806`c0788000   storqosflt   (deferred)
```

**已附加调试器的启动**

如果可以在已连接调试器的情况下启动目标系统，则在发生错误检测时，请发出 [**！ devnode 0 1**](-devnode.md) 。 你将看到哪个设备缺少驱动程序或无法启动，并且无法启动的原因可能会很明显。

其中一个原因可能是即插即用无法将资源分配给启动设备。 可以通过查找服务的条目来验证此限制。 如果状态标志包括 DNF \_ 资源不足 \_ ，或者不包括 DNF \_ 已启动或 DNF \_ 枚举，则可能是因为找到了问题。 请尝试 **！ devnode 0 1 storahci** 保存一些时间，而不是转储整个设备树。

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

 

 




