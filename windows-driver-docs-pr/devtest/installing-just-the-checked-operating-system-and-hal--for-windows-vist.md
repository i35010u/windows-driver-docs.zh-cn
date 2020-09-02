---
title: 仅安装已检查的操作系统和 HAL
description: 只安装已检验的操作系统和 HAL（适用于 Windows Vista 和更高版本）
ms.assetid: 1203b7cd-50b9-4174-8bec-112019444fac
ms.date: 05/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 7ea193c8724b09360ff17cfcdf1a1d08e030bc62
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382917"
---
# <a name="installing-just-the-checked-operating-system-and-hal-for-windows-vista-and-later"></a>只安装已检验的操作系统和 HAL（适用于 Windows Vista 和更高版本）

> [!NOTE]
> 在 Windows 10 版本1803之前，已检查的生成在较早版本的 Windows 上可用。
> 使用驱动程序验证程序和 GFlags 等工具在更高版本的 Windows 中检查驱动程序代码。

您无需在您的计算机上安装完整的检查生成，而可以安装系统的免费版本，然后安装操作系统映像和硬件抽象层的已检查版本 (HAL) 。 如果你使用此过程，则可以配置引导加载程序，以便为你提供两个启动选项。 一个引导选项用于免费生成。 第二个启动选项使用所选的操作系统映像和 HAL 启动系统，但使用所有其他系统组件的免费版本。

## <a name="step-1---identifying-the-files-to-install-for-windows-vista-and-later"></a>步骤 1-确定要安装的 Windows Vista 和更高版本的文件

在安装部分检查版本之前，必须确定用于在系统上安装免费版本的操作系统映像和 HAL 文件的版本。

**提示**   对于64位版本的 Windows Vista 和更高版本，此过程非常简单。 如果使用 [Windows 驱动程序工具包 (wdk) ](../index.yml)，则可以使用 wdk 的 "调试" 目录中的操作系统映像和 HAL 文件 \\ 。 请参阅 [安装检查的生成](installing-the-checked-build.md)。 对于 amd64 或 ia64，每个只有一个版本。 文件的名称是 ntkrnlmp.exe 和 Hal.dll。 如果你使用的是适用于你的 Windows 版本的 WDK，则可以跳到 [步骤2：复制已检查的文件](#step-2---copying-the-checked-files)。

 

在运行32位版本 Windows 的计算机上，使用以下过程来确定要复制的文件的名称：

### <a name="determining-the-name-of-the-hal-that-is-installed"></a>确定安装的 HAL 的名称

1.  打开文件% SystemRoot% \\ Inf \\ setupapi.log 并搜索 hal.dll。

    应该会看到一条类似于 TargetFilename 的行-' hal.dll

2.  在日志文件的同一节中，查找相应的 *SourceFilename*。 *SourceFilename*右侧的名称是需要从所选版本复制的 HAL 文件的名称。

下面的示例来自 setupapi.log 文件。 *SourceFilename* halmacpi.dll：

```
{FILE_QUEUE_COPY}
   CopyStyle      - 0x09180000
   SourceRootPath - 'C:\Windows\System32\DriverStore\FileRepository\hal.inf_0c52392f'
   SourceFilename - 'halmacpi.dll'
   TargetDirectory- 'C:\Windows\system32'
   TargetFilename - 'hal.dll'
   SourceDesc     - 'windows cd'
{FILE_QUEUE_COPY exit(0x00000000)}
```

### <a name="determining-the-name-of-the-operating-system-image-file-installed"></a>确定安装的操作系统映像文件的名称

对于64位版本的 Windows Vista 和更高版本，ntkrnlmp.exe 该文件的名称。

对于32位版本的 Windows Vista，你可以使用以下过程来确定是否安装了单处理器或多处理器版本。

1.  在计算机管理控制台中打开 "事件查看器" (compmgmt.msc) "。

2.  在系统日志中查找事件 ID 6009。

    此事件的属性指示您是安装了单个处理器还是多处理器版本的操作系统映像。

例如，下面的示例指示提供多处理器支持的操作系统的免费版本。

```
Microsoft (R) Windows (R) 6.00. 6001 Service Pack 1 Multiprocessor Free.
```

如果知道处理器类型和计算机上安装的物理内存量，则可以从以下项之一中选择映像名称。 如果已附加内核调试器，还可以使用 **lmv mnt** 命令来标识原始文件名。

<span id="NTOSKRNL.EXE"></span>ntoskrnl.exe  
4 GB 或更小物理内存的单处理器 x86 体系结构系统。

<span id="NTKRNLPA.EXE"></span>ntkrnlpa.exe  
具有 PAE 支持的单处理器 x86 体系结构系统。

<span id="NTKRNLMP.EXE"></span>ntkrnlmp.exe  
多处理器 x86 体系结构系统，物理内存不超过 4 GB。

<span id="NTKRPAMP.EXE"></span>ntkrpamp.exe  
具有 PAE 支持的多处理器 x86 体系结构系统。

## <a name="step-2---copying-the-checked-files"></a>步骤 2-复制选定的文件

现在，你知道在系统安装过程中使用的文件的名称，你可以将这些文件的已检查版本复制到系统中。 在 WDK 的 "调试" 目录中，或在 "已检查分发包" 中查找已标识的文件。 然后将这些文件复制到系统的% SystemRoot% \\ system32 目录，并为其提供新的、唯一的文件名。 确保文件名唯一的一种方法是：在复制文件类型时，将文件类型从其原始文件类型重命名为 ( .dll 或 .exe) 为 .chk。 因此，使用步骤1中的示例，您可以从已检查的分发工具包复制文件，如下所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">如果 WDK 的 "调试" 目录中的原始文件名为：</th>
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
<tr class="even">
<td align="left"><p>hal.dll</p></td>
<td align="left"><p>hal .chk</p></td>
</tr>
</tbody>
</table>

 

## <a name="step-3---changing-the-boot-parameters-using-bcdedit"></a>步骤 3-使用 BCDEdit 更改启动参数

将检查的文件复制到% SystemRoot% \\ system32 目录之后，必须创建一个启动时条目，以便系统可以开始使用这些已检查的文件。 您可以使用 BCDEdit 来创建此。

**提示**   你可以复制现有启动条目以创建新的启动条目，你可以修改该条目以使用已检查的操作系统映像和 HAL。 例如，若要创建当前启动项的副本，请使用以下命令： **bcdedit/copy {current}/d "Windows 8.1 部分检查版本"**。
有关使用 BCDEdit 的一般说明，请参阅用于 [更改驱动程序测试和调试的启动选项](boot-options-for-driver-testing-and-debugging.md) 和 [编辑启动选项](editing-boot-options.md)的工具。

**注意**   设置 BCDEdit 选项之前，你可能需要在计算机上禁用或暂停 BitLocker 和安全启动。

 
若要在 Windows Vista 和更高版本上配置部分检查的生成，请使用 [**BCDEdit/set**](./bcdedit--set.md) 命令和 **内核** 和 **hal** 选项。

例如，以下命令将配置启动项以使用已检查的内核和 HAL 版本。

```
bcdedit /set {44a942bf-d6ee-11e3-baf8-000ffee4f6cd} kernel ntkrnlmp.chk
```

```
bcdedit /set {44a942bf-d6ee-11e3-baf8-000ffee4f6cd} hal hal.chk
```

还必须将计算机配置为进行内核调试。 具体而言，必须为启动调试 [**BCDEdit/bootdebug**](./bcdedit--bootdebug.md)启用启动项。 如果未启用启动调试，并且没有将内核调试器连接到计算机，则当你选择此新的启动条目时，计算机将启动到 Windows 恢复环境中。

```
bcdedit /bootdebug {44a942bf-d6ee-11e3-baf8-000ffee4f6cd} on
```

若要查看命令的结果，请键入 **bcdedit/enum**。 **/Enum**选项列出所有启动项。 例如，已将以下启动条目修改为使用所选版本的内核和 HAL。 还必须在) 上启用启动调试 (bcdedit/bootdebug {ID} 的启动项。

```
## Windows Boot Loader
-------------------
identifier              {44a942bf-d6ee-11e3-baf8-000ffee4f6cd}
device                  partition=C:
path                    \Windows\system32\winload.exe
description             Windows 8.1 Partial Checked Build
locale                  en-US
inherit                 {bootloadersettings}
recoverysequence        {44a942bd-d6ee-11e3-baf8-000ffee4f6cd}
integrityservices       Disable
recoveryenabled         Yes
bootdebug               Yes
testsigning             Yes
allowedinmemorysettings 0x15000075
osdevice                partition=C:
systemroot              \Windows
kernel                  ntkrnlmp.chk
hal                     hal.chk
resumeobject            {44a942bb-d6ee-11e3-baf8-000ffee4f6cd}
nx                      OptIn
bootmenupolicy          Standard
debug                   Yes
```

## <a name="step-4---restart-the-computer"></a>步骤 4-重新启动计算机

进行更改后，将计算机配置为进行内核调试，启用启动调试，并将内核调试器连接起来。 重新启动计算机。 当你重新启动计算机时，将显示一个新的操作系统启动选项，允许你选择所选的操作系统映像和 HAL。

你可以使用以下过程来验证是否正在运行检查生成。

1.  在计算机管理控制台中打开 "事件查看器" (compmgmt.msc) "。

2.  在系统日志中查找事件 ID 6009。

    此事件的属性指示是否已安装操作系统映像的免费或已检查版本。

例如，以下事件的描述表明具有多处理器支持的操作系统的已检查版本。

```
Microsoft (R) Windows (R) 6.00. 6001 Service Pack 1 Multiprocessor Checked.
```

## <a name="related-topics"></a>相关主题


[设置调试（内核模式和用户模式）](../debugger/getting-set-up-for-debugging.md)

[Windows 调试工具](../debugger/index.md)

 

