---
title: 安装检查的操作系统和 HAL （Windows XP 和 Windows Server 2003）
description: 只安装已检验的操作系统和 HAL（适用于 Windows XP 和 Windows Server 2003）
ms.assetid: 51175951-9267-4d92-8b47-4dd2155f4e56
keywords:
- 检查内部版本号 WDK，安装
- 免费生成 WDK
- 零售生成 WDK
- HAL WDK
- 部分选中的生成 WDK
- 检查生成名称 WDK
- 复制已检查的文件
- Boot.ini 文件 WDK，检查生成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e5dd6eaaccd860590e7801278a757461f7b0de0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356593"
---
# <a name="installing-just-the-checked-operating-system-and-hal-for-windows-xp-and-windows-server-2003"></a>只安装已检验的操作系统和 HAL（适用于 Windows XP 和 Windows Server 2003）


## <span id="ddk_installing_just_the_checked_operating_system_and_hal_tools"></span><span id="DDK_INSTALLING_JUST_THE_CHECKED_OPERATING_SYSTEM_AND_HAL_TOOLS"></span>


而不是在计算机上安装完整的调试内部版本，你可以安装的系统，免费版，然后安装操作系统映像和 HAL 的付费版本。 如果您使用此过程，您可以配置引导加载程序为你提供两个启动选项。 第一个启动选项适用于免费版。 第二个启动选项启动系统使用选中的操作系统映像和 HAL，但使用免费版本的所有其他系统组件。

此方法时，与安装完整的调试内部版本，相比具有以下优点：

-   驱动程序获得的操作系统和 HAL 调试检查的好处。 在同一时间，因为正在使用免费版本的操作系统和 HAL 以外的系统组件，对整个系统的性能影响最小化。

-   单个安装 （并因此一个系统目录、 一组可执行组件和一组注册表参数） 可以使用已检查或免费版本的操作系统映像和 HAL，确定在启动时。

若要安装的操作系统映像和 HAL 付费版本，你必须将复制相应的文件从选中的分发介质到 %systemroot%\\system32 目录中使用新的、 唯一的文件的名称。 然后，您必须指示系统以提供在系统启动过程中使用这些文件的选项。 您应记住以下重要准则否则为免费安装上安装已检查的操作系统和 HAL 图像时：

-   操作系统映像和 HAL 必须保持同步在所有时间。 因此，如果使用操作系统映像的经检查的版本，还必须使用的经检查的版本的 HAL （反之亦然）。 无法将系统的操作系统映像和协调的 HAL 可以使系统无法启动。

-   不会覆盖在免费版本的安装过程中安装免费版本的操作系统映像和 HAL。 操作系统映像和 HAL 的覆盖的免费版本可能会使系统无法启动，并可以使难以从错误中恢复。 因此，始终要小心使用新的唯一文件名的操作系统和 HAL 付费版本复制到 %systemroot%时\\system32 目录。

-   请确保选中的分发使用是免费的系统的 Service Pack 数相同。 例如，如果系统安装免费版本的 Service Pack 2 的系统上安装已检查的操作系统映像和 HAL，确保选中的分发使用也是 Service Pack 2。

若要安装部分已检验的版本的步骤如下所示：

### <a name="span-idstep_1__identifying_the_files_to_installspanspan-idstep_1__identifying_the_files_to_installspanstep-1-identifying-the-files-to-install"></a><span id="step_1__identifying_the_files_to_install"></span><span id="STEP_1__IDENTIFYING_THE_FILES_TO_INSTALL"></span>步骤 1:确定要安装的文件

安装部分已检验的版本的第一步是确定的操作系统映像和 HAL 文件用于在系统上安装免费的生成版本。

基于 NT 的操作系统分发介质上提供了几个不同版本的操作系统和 HAL 图像。 这些不同的版本存在以支持的处理器和其他系统硬件的不同组合。 在安装操作系统软件后，安装过程中自动确定哪些操作系统映像和到使用，并将相应的文件复制到系统的 %systemroot%分发介质中的 HAL 映像\\system32 目录。

安装操作系统映像文件取决于一个或多个处理器是否受到支持，以及是否支持物理地址扩展 (PAE) （PAE 处于活动状态超过 4 gb 的物理内存的系统上）。 分发介质上的文件名称如下所示：

<span id="NTOSKRNL.EXE"></span>ntoskrnl.exe  
具有 4 GB 的物理内存或更短的单处理器 x86 体系结构系统。

<span id="NTKRNLPA.EXE"></span>ntkrnlpa.exe  
PAE 支持单处理器 x86 体系结构系统。

<span id="NTKRNLMP.EXE"></span>ntkrnlmp.exe  
多处理器 x86 体系结构具有 4 GB 的物理内存或更少的系统。

<span id="NTKRPAMP.EXE"></span>ntkrpamp.exe  
PAE 支持多处理器 x86 体系结构系统。

同样，名称有多个不同的 HAL。

在系统安装的安装过程确定适当的操作系统映像和 HAL，若要在系统上安装。 所选的文件复制到 %systemroot%\\system32 目录在安装期间，使用固定的、 众所周知的名称。 使用这些固定名称轻松加载程序在启动时找到这些文件。 这些文件的固定的名称为：

<span id="NTOSKRNL.EXE"></span>ntoskrnl.exe  
适用于 x86 的操作系统映像具有 4 GB 的物理内存或更少的系统。

<span id="NTKRNLPA.EXE"></span>ntkrnlpa.exe  
适用于 x86 的操作系统映像具有超过 4GB 的物理内存的系统。

<span id="HAL.DLL"></span>hal.dll  
可加载 HAL 图像。

请注意，在某些情况下，具体取决于系统的硬件配置一个或多个文件可能会重命名为适当的固定名称。 在其他情况下，分发介质上的文件名称是必需的固定的文件名称相同。

若要安装的已检查的操作系统映像和 HAL，必须首先确定已复制到您的系统在系统安装过程中的图像的原始名称。 若要执行此操作，请检查文件 %systemroot%\\修复\\setup.log。 这是一个隐藏的文件，因此您需要更改其属性，然后才能查看它使用**dir**命令。

Setup.log 文件列出了从分发介质复制到 %systemroot%的文件\\在安装过程中系统的 system32 目录。

Setup.log 文件的示例如下所示：

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

在示例 setup.log 文件中，可以看到两个操作系统映像文件已复制到\\winnt\\system32 目录 (即 %systemroot%\\system32) 在安装过程中。 文件 ntkrpamp.exe 从分发介质复制到 ntkrnlpa.exe 和文件 ntkrnlmp.exe 从分发介质复制到 ntoskrnl.exe。 从本示例中，您还可以看到 HAL 文件 (与在 %systemroot%固定的名称 hal.dll\\system32 目录) 最初名为 halmacpi.dll。

**警告**  一些 HAL 文件具有非常相似的名称。 例如，halacpi.dll 和 halapic.dll 是两个常用的 Hal。 请务必使用正确版本的 HAL，为您的系统。 选择错误的 HAL 将导致不是可启动的系统。

 

### <a name="span-idstep_2__copying_the_checked_filesspanspan-idstep_2__copying_the_checked_filesspanstep-2-copying-the-checked-files"></a><span id="step_2__copying_the_checked_files"></span><span id="STEP_2__COPYING_THE_CHECKED_FILES"></span>步骤 2:复制所选的文件

现在，在系统安装过程中了解所使用的文件的名称，您可以将这些文件的付费版本复制到您的系统。 选中的分发工具包中找到具有标识的文件。 然后将这些文件复制到 %systemroot%\\system32 目录的系统，为他们提供新的、 唯一的文件的名称。 这些文件的副本必须遵循 8.3 命名约定。 若要确保唯一且符合 8.3 文件名称的一种方法是重命名从其原始的文件类型 （.dll 或.exe） 文件类型.chk 复制时。 因此，在步骤 1 中使用的示例，你会将文件复制选中的分发工具包中，如下所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">如果选中分发中的原始文件名称为：</th>
<th align="left">将其复制到 %systemroot%\system32 中的以下文件名称：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ntkrnlmp.exe</p></td>
<td align="left"><p>ntkrnlmp.chk</p></td>
</tr>
<tr class="even">
<td align="left"><p>ntkrpamp.exe</p></td>
<td align="left"><p>ntkrpamp.chk</p></td>
</tr>
<tr class="odd">
<td align="left"><p>halmapic.dll</p></td>
<td align="left"><p>halmapic.chk</p></td>
</tr>
</tbody>
</table>

 

选中分发中的某些文件的压缩形式提供。 下划线字符的情况下为它们的文件类型中的最后一个字符来指示这些文件。 例如，如果您查看的文件 halapic.dll 已检验的版本分发工具包中，您将发现文件 halapic.dl\_，这是正确的文件，但以压缩形式。

若要解压缩压缩的文件从选中分发，使用展开实用工具 (%systemroot%\\system32\\expand.exe)。 例如，若要展开 halapic.dl\_和名称作为 halapic.chk 展开的文件，可以从命令提示符窗口使用以下命令：

```
> expand halapic.dl_ halapic.chk
```

### <a name="span-idstep_3__editing_boot_inispanspan-idstep_3__editing_boot_inispanstep-3-editing-bootini"></a><span id="step_3__editing_boot_ini"></span><span id="STEP_3__EDITING_BOOT_INI"></span>步骤 3:编辑 boot.ini

选中的文件复制到 %systemroot%后\\system32 目录中，您必须创建一个允许系统以开始使用这些已检查的文件的启动时间选项。 若要执行此操作，编辑 boot.ini 文件。

有关常规说明，请参阅[编辑 boot.ini 文件](editing-the-boot-ini-file.md)。

在此特定情况下，您需要创建新的启动时间选项，可用于启动系统，请使用操作系统映像和已安装的 HAL 的经检查版本。

找到在行 **\[操作系统\]** 部分指的是 Windows 安装的 boot.ini。 创建第二个副本，并将以下参数添加到复制行的末尾：

```
/kernel=KernelFile /hal=HalFile 
```

其中*KernelFile*是通过选中的分发工具包先前复制的操作系统映像文件的经检查版本的名称和*HalFile*的经检查版本的名称从选中的分发工具包以前复制的 HAL。

如果描述您的操作系统的行包含 **/PAE**参数，请确保使用具有 PAE 支持的操作系统映像的经检查的版本。 描述您的操作系统的行没有 **/PAE**参数，请使用操作系统的经检查的版本映像没有 PAE 支持。

因此，可以确定哪些行是免费版本和哪些行是部分已检验的版本，还应更改的新行上的带引号的文本。

此类的 boot.ini 文件的示例如下所示：

```
[boot loader]
timeout=30
default=multi(0)disk(0)rdisk(0)partition(1)\WINNT
[operating systems]
multi(0)disk(0)rdisk(0)partition(1)\WINNT="Microsoft Windows 2000 Professional" /fastdetect
multi(0)disk(0)rdisk(0)partition(1)\WINNT="Windows 2000 Checked" /fastdetect /kernel=ntoskrnl.chk /hal=halacpi.chk
```

如果使用内核调试程序调试内部版本，则还应添加与调试相关的正确参数。 ( **/Kernel**并 **/hal**参数不会启用自动调试。)有关详细信息，请参阅[编辑 boot.ini 文件](editing-the-boot-ini-file.md)。

所做的更改之后，保存所做的更改并退出编辑器。 下一次启动此系统中，将显示，可选择选中的操作系统映像和 HAL 的新的操作系统启动选项。

### <a name="span-idinstalling_additional_checked_filesspanspan-idinstalling_additional_checked_filesspaninstalling-additional-checked-files"></a><span id="installing_additional_checked_files"></span><span id="INSTALLING_ADDITIONAL_CHECKED_FILES"></span>安装已检查的其他文件

检查的操作系统和 HAL 安装后，您可以通过安装其他选中的组件。 可以使用从选中的分发介质选中对应替换几个关键组件的已安装的免费版本。 这可以是很有用，例如，你编写在其他设备的堆栈中存在的驱动程序时。 通过将替换为所上方和下方您的驱动程序堆栈中的驱动程序的免费版本，将启用检查这些组件中的其他错误。 这可以帮助您更快速、 轻松地识别您的驱动程序中的问题。

替换时可用的驱动程序对应的检查，没有方法来轻松地为系统提供的驱动程序组件提供替代图像。 因此时您免费驱动程序将替换为已检查驱动程序在系统上，, 选中的驱动程序将使用是免费或检查版本的操作系统映像和 HAL 启动时。 因此，你可能想要重命名 （或复制） 将其选中对应项，替换为任何驱动程序的原始免费版本，以便以后还原免费驱动程序。

最后，请注意，任何时候您更改某个系统目录中存在的标准文件之一 (如 %systemroot%\\system32) Windows 文件保护 (WFP) 将为其原始状态还原该文件，除非先禁用 WFP。 如果调试程序附加到您的系统，您可以通过更改以下注册表值来临时禁用 WFP:

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon
SFCDisable:REG_DWORD:2
```

设置**SFCDisable**值为 2 的下一次启动 （仅限） 禁用 WFP。 值为 0 （默认值） 启用 WFP。 有关 WFP 的功能的说明，请参阅 Microsoft Windows SDK。 有关 WFP 注册表设置的详细信息，请参阅[Microsoft 知识库文章 Q222473](https://go.microsoft.com/fwlink/p/?linkid=38360)。

 

 





