---
title: '在 Windows XP 和 Windows Server 2003 (安装检查的操作系统和 HAL) '
description: 只安装已检验的操作系统和 HAL（适用于 Windows XP 和 Windows Server 2003）
keywords:
- 已检查生成 WDK，安装
- 免费生成 WDK
- 零售版本 WDK
- HAL WDK
- 部分检查的生成 WDK
- 命名 WDK 检查版本
- 复制检查的文件
- Boot.ini 文件 WDK，已检查版本
ms.date: 05/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: ad9929dcfba101e988bd936d9535f6b274cc3317
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813883"
---
# <a name="installing-just-the-checked-operating-system-and-hal-for-windows-xp-and-windows-server-2003"></a>只安装已检验的操作系统和 HAL（适用于 Windows XP 和 Windows Server 2003）

> [!NOTE]
> 在 Windows 10 版本1803之前，已检查的生成在较早版本的 Windows 上可用。
> 使用驱动程序验证程序和 GFlags 等工具在更高版本的 Windows 中检查驱动程序代码。

## <span id="ddk_installing_just_the_checked_operating_system_and_hal_tools"></span><span id="DDK_INSTALLING_JUST_THE_CHECKED_OPERATING_SYSTEM_AND_HAL_TOOLS"></span>

您无需在您的计算机上安装完整的检查生成，而可以安装系统的免费版本，然后安装操作系统映像和 HAL 的已检查版本。 如果你使用此过程，则可以配置引导加载程序，以便为你提供两个启动选项。 第一个启动选项用于免费生成。 第二个启动选项使用所选的操作系统映像和 HAL 启动系统，但使用所有其他系统组件的免费版本。

与安装完整的已选中版本相比，这种方法具有以下优点：

-   驱动程序可以获得操作系统和 HAL 调试检查的好处。 同时，由于使用的系统组件的版本不是操作系统和 HAL，因此，对整个系统的性能影响将降到最低。

-   单个安装 (，因此一个系统目录、一组可执行组件和一组注册表参数) 可以使用操作系统映像和 HAL 的已检查版本或免费版本（在启动时确定）。

若要安装操作系统映像和 HAL 的已检查版本，必须使用新的、唯一的文件名将相应的文件从已检查的分发媒体复制到% SystemRoot% \\ system32 目录。 然后，必须指示系统在系统启动期间提供一个使用这些文件的选项。 在其他免费安装上安装已检查的操作系统和 HAL 映像时，应记住以下重要准则：

-   操作系统映像和 HAL 必须始终保持同步。 因此，如果使用操作系统映像的已检查版本，则还必须使用所选的 HAL 版本 (，反之亦然) 。 未能使系统的操作系统映像和 HAL 进行协调会使系统无法启动。

-   不要覆盖操作系统映像和安装免费版本期间安装的 HAL 的免费版本。 覆盖操作系统映像和 HAL 的免费版本可能使系统无法启动，并可能会导致难以从错误中恢复。 因此，在将操作系统和 HAL 的已检查版本复制到% SystemRoot% system32 目录时，请务必谨慎使用新的唯一文件名 \\ 。

-   请确保所使用的选定分发版与免费系统的服务包号相同。 例如，如果在安装了免费生成系统的 Service Pack 2 的系统上安装已检查操作系统映像和 HAL，请确保所使用的已检查分发也是 Service Pack 2。

安装部分检查的生成的步骤如下所示：

### <a name="span-idstep_1__identifying_the_files_to_installspanspan-idstep_1__identifying_the_files_to_installspanstep-1-identifying-the-files-to-install"></a><span id="step_1__identifying_the_files_to_install"></span><span id="STEP_1__IDENTIFYING_THE_FILES_TO_INSTALL"></span>步骤1：确定要安装的文件

安装部分检查版本的第一步是确定用于在系统上安装免费版本的操作系统映像和 HAL 文件的版本。

基于 NT 的操作系统分发介质上提供了几种不同版本的操作系统和 HAL 映像。 这些不同版本的存在是为了支持处理器和其他系统硬件的不同组合。 安装操作系统软件时，安装过程会自动标识要使用的操作系统映像和 HAL 映像，并将相应的文件从分发介质复制到系统的% SystemRoot% \\ system32 目录。

安装的操作系统映像文件取决于是否支持一个或多个处理器，并确定物理地址扩展 (PAE) 是否受支持 (PAE 在物理内存) 超过 4 GB 的系统上是否处于活动状态。 分发介质上的文件名如下：

<span id="NTOSKRNL.EXE"></span>ntoskrnl.exe  
4 GB 或更小物理内存的单处理器 x86 体系结构系统。

<span id="NTKRNLPA.EXE"></span>ntkrnlpa.exe  
具有 PAE 支持的单处理器 x86 体系结构系统。

<span id="NTKRNLMP.EXE"></span>ntkrnlmp.exe  
多处理器 x86 体系结构系统，物理内存不超过 4 GB。

<span id="NTKRPAMP.EXE"></span>ntkrpamp.exe  
具有 PAE 支持的多处理器 x86 体系结构系统。

同样，HAL 有多个不同的名称。

在系统安装过程中，安装过程会确定要在您的系统上安装的相应操作系统映像和 HAL。 使用固定的已知名称，在安装过程中将所选文件复制到% SystemRoot% \\ system32 目录。 使用这些固定名称可以使加载程序在启动时轻松找到这些文件。 这些文件的固定名称为：

<span id="NTOSKRNL.EXE"></span>ntoskrnl.exe  
适用于物理内存不超过 4 GB 的 x86 系统的操作系统映像。

<span id="NTKRNLPA.EXE"></span>ntkrnlpa.exe  
物理内存超过 4 GB 的 x86 系统的操作系统映像。

<span id="HAL.DLL"></span>hal.dll  
可加载的 HAL 映像。

请注意，在某些情况下，根据系统的硬件配置，可以将一个或多个文件重命名为适当的固定名称。 在其他情况下，分发介质上的文件名与所需的固定文件名相同。

若要安装所选的操作系统映像和 HAL，你必须首先确定系统安装过程中复制到系统中的映像的原始名称。 若要执行此过程，请检查文件% SystemRoot% \\ repair \\ setup .log。 这是一个隐藏文件，因此你需要更改其属性，然后才能使用 **dir** 命令查看它。

安装日志文件列出系统安装过程中从分发介质复制到% SystemRoot% system32 目录的文件 \\ 。

安装日志文件的示例如下所示：

```
[Paths]
TargetDirectory = "\WINNT"
TargetDevice = "\Device\Harddisk0\Partition1"
SystemPartitionDirectory = "\"
SystemPartition = "\Device\Harddisk0\Partition1"
[Signature]
Version = "WinNt5.1"
[Files.SystemPartition]
NTDETECT.COM = "NTDETECT.COM","f41f"
ntldr = "ntldr","3e8b5"
arcsetup.exe = "arcsetup.exe","379db"
arcldr.exe = "arcldr.exe","2eca9"
[Files.WinNt]
\WINNT\system32\drivers\kbdclass.sys = "kbdclass.sys","e259"
\WINNT\system32\drivers\mouclass.sys = "mouclass.sys","7e78"
\WINNT\system32\drivers\uhcd.sys = "uhcd.sys","10217"
\WINNT\system32\drivers\usbd.sys = "usbd.sys","5465"
(...several similar lines omitted...)
\WINNT\system32\framebuf.dll = "framebuf.dll","10c84"
\WINNT\system32\hal.dll = "halmacpi.dll","2bedf"
\WINNT\system32\ntkrnlpa.exe = "ntkrpamp.exe","1d66a6"
\WINNT\system32\ntoskrnl.exe = "ntkrnlmp.exe","1ce5c5"
\WINNT\inf\mdmrpci.inf = "mdmrpci.inf","96a3"
```

在示例安装程序 .log 文件中，可以看到两个操作系统镜像文件已复制到 \\ winnt \\ system32 目录 (在安装过程中，这是% SystemRoot% \\ system32) 。 文件 ntkrpamp.exe 从分发介质复制到 ntkrnlpa.exe，并且文件 ntkrnlmp.exe 从分发介质复制到 ntoskrnl.exe。 在此示例中，你还可以看到，在% SystemRoot% \\ system32 目录) 最初名为 halmacpi.dll 的 HAL 文件 (具有固定名称 hal.dll。

**警告**   某些 HAL 文件具有其实不然相似名称。 例如，halacpi.dll 和 halapic.dll 是两个常用的 Hal。 请注意，使用正确版本的 HAL 作为系统。 选择错误的 HAL 将导致系统无法引导。

 

### <a name="span-idstep_2__copying_the_checked_filesspanspan-idstep_2__copying_the_checked_filesspanstep-2-copying-the-checked-files"></a><span id="step_2__copying_the_checked_files"></span><span id="STEP_2__COPYING_THE_CHECKED_FILES"></span>步骤2：复制已检查的文件

现在，你知道在系统安装过程中使用的文件的名称，你可以将这些文件的已检查版本复制到系统中。 查找在已检查的分发工具包中标识的文件。 然后将这些文件复制到系统的% SystemRoot% \\ system32 目录，并为其提供新的、唯一的文件名。 这些文件的副本必须遵循8.3 命名约定。 确保符合8.3 的唯一文件名的一种方法是：在复制文件类型时，将文件类型从其原始文件类型重命名为 ( .dll 或 .exe) 。 因此，使用步骤1中的示例，您可以从已检查的分发工具包复制文件，如下所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">如果检查的分发中的原始文件名为：</th>
<th align="left">将其复制到%SystemRoot%\system32 中的以下文件名：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ntkrnlmp.exe</p></td>
<td align="left"><p>ntkrnlmp</p></td>
</tr>
<tr class="even">
<td align="left"><p>ntkrpamp.exe</p></td>
<td align="left"><p>ntkrpamp</p></td>
</tr>
<tr class="odd">
<td align="left"><p>halmapic.dll</p></td>
<td align="left"><p>halmapic</p></td>
</tr>
</tbody>
</table>

 

已检查分发中的某些文件以压缩形式提供。 这些文件使用下划线字符作为其文件类型中的最后一个字符。 例如，如果在 "已检查的生成分发包" 中查找文件 halapic.dll，则会找到文件 halapic \_ ，它是正确的文件，但采用压缩形式。

若要从选定的分发中解压缩压缩文件，请使用展开实用工具 (% SystemRoot% \\ system32 \\expand.exe) 。 例如，若要展开 halapic \_ 并将展开的文件命名为 halapic，可以在命令提示符窗口中使用以下命令：

```
> expand halapic.dl_ halapic.chk
```

### <a name="span-idstep_3__editing_boot_inispanspan-idstep_3__editing_boot_inispanstep-3-editing-bootini"></a><span id="step_3__editing_boot_ini"></span><span id="STEP_3__EDITING_BOOT_INI"></span>步骤3：编辑 boot.ini

将所选文件复制到% SystemRoot% \\ system32 目录后，必须创建启动时选项，使系统能够开始使用这些已检查的文件。 若要执行此，请编辑 boot.ini 文件。

有关一般说明，请参阅 [编辑 boot.ini 文件](editing-the-boot-ini-file.md)。

在此特定情况下，你需要创建一个新的引导时选项，该选项允许你使用已安装的操作系统映像和 HAL 的已检查版本启动系统。

在引用您的 Windows 安装的 boot.ini 的 " **\[ 操作系统 \]** " 部分找到该行。 创建它的第二个副本，并将以下参数添加到复制行的末尾：

```
/kernel=KernelFile /hal=HalFile 
```

其中， *KernelFile* 是以前从已检查的分发工具包中复制的操作系统映像文件的已检查版本的名称， *HalFile* 是以前从已检查的分发工具包中复制的 HAL 的已检查版本的名称。

如果描述操作系统的行包含 **/pae** 参数，请确保使用具有 PAE 支持的操作系统映像的已检查版本。 如果描述操作系统的行没有 **/pae** 参数，请使用没有 PAE 支持的操作系统映像的已检查版本。

还应更改新行上的带引号文本，以便您可以确定哪个行是免费生成，哪一行是部分检查的生成。

此类 boot.ini 文件的示例如下所示：

```
[boot loader]
timeout=30
default=multi(0)disk(0)rdisk(0)partition(1)\WINNT
[operating systems]
multi(0)disk(0)rdisk(0)partition(1)\WINNT="Microsoft Windows 2000 Professional" /fastdetect
multi(0)disk(0)rdisk(0)partition(1)\WINNT="Windows 2000 Checked" /fastdetect /kernel=ntoskrnl.chk /hal=halacpi.chk
```

如果将检查的生成用于内核调试器，还应添加与调试相关的正确参数。  (**/kernel** 和 **/hal** 参数不会自动启用调试 ) 。有关详细信息，请参阅 [编辑 boot.ini 文件](editing-the-boot-ini-file.md)。

进行更改后，保存所做的更改并退出编辑器。 下一次启动此系统时，将显示一个新的操作系统启动选项，使你能够选择所选的操作系统映像和 HAL。

### <a name="span-idinstalling_additional_checked_filesspanspan-idinstalling_additional_checked_filesspaninstalling-additional-checked-files"></a><span id="installing_additional_checked_files"></span><span id="INSTALLING_ADDITIONAL_CHECKED_FILES"></span>安装其他检查的文件

安装了所选的操作系统和 HAL 后，可以选择安装其他选中的组件。 您可以将几个关键组件的已安装、免费版本替换为选中的分发介质的已选中的对应项。 例如，当你在其他设备的堆栈中编写的驱动程序时，这会很有帮助。 通过替换堆栈中驱动程序上方和下方的驱动程序的免费版本，你将在这些组件中启用其他错误检查。 这可以帮助您更快、更轻松地识别您的驱动程序中的问题。

将可用驱动程序替换为其选中的对应项时，无法为系统提供的驱动程序组件轻松提供备用映像。 因此，当你在系统上将可用驱动程序替换为所选的驱动程序时，在启动操作系统映像包和 HAL 的免费或已检查版本时，将使用所选的驱动程序。 因此，您可能希望重命名 (或复制) 您替换为其选中的对应项的任何驱动程序的原始免费版本，以便以后可以还原免费的驱动程序。

最后请注意，只要将某个系统 (目录中存在的某个标准文件（例如% SystemRoot% system32）更改为% SystemRoot% \\ system32) Windows 文件保护 (WFP) 就会将该文件还原到其原始状态，除非第一次禁用 wfp。 如果将调试器附加到系统，则可以通过更改以下注册表值来暂时禁用 WFP：

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon
SFCDisable:REG_DWORD:2
```

如果将 **SFCDisable** 设置为值2，则仅对下一次启动 (禁用 WFP) 。 值 0 (默认) 启用 WFP。 有关 WFP 功能的说明，请参阅 Microsoft Windows SDK。

 

 





