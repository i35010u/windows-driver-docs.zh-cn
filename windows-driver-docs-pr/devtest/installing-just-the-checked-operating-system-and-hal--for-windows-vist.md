---
title: 安装只需检查的操作系统和 HAL
description: 只安装已检验的操作系统和 HAL（适用于 Windows Vista 和更高版本）
ms.assetid: 1203b7cd-50b9-4174-8bec-112019444fac
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 727cebe2bbe3f3a4f324428501c9d06f87c29ddf
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349213"
---
# <a name="installing-just-the-checked-operating-system-and-hal-for-windows-vista-and-later"></a>只安装已检验的操作系统和 HAL（适用于 Windows Vista 和更高版本）


而不是在计算机上安装完整的调试内部版本，你可以安装的系统，免费版，然后安装操作系统映像和硬件抽象层 (HAL) 的付费版本。 如果您使用此过程，您可以配置引导加载程序为你提供两个启动选项。 一个启动选项适用于免费版。 第二个启动选项启动系统使用选中的操作系统映像和 HAL，但使用免费版本的所有其他系统组件。

## <a name="step-1---identifying-the-files-to-install-for-windows-vista-and-later"></a>步骤 1-确定安装适用于 Windows Vista 及更高版本的文件

在安装部分已检验的版本之前，必须确定版本的操作系统映像和 HAL 文件用于在系统上安装免费的生成。

**提示**  于 64 位版本的 Windows Vista 及更高版本中，此过程非常简单。 如果有[Windows Driver Kit (WDK)](https://msdn.microsoft.com/library/windows/hardware/ff557573)，可以使用的操作系统映像和从调试的 HAL 文件\\WDK 的目录。 请参阅[安装已检验的版本](installing-the-checked-build.md)。 没有为 amd64 或 ia64 每个只有一个版本。 文件的名称是 ntkrnlmp.exe 和 Hal.dll。 如果你使用的 Windows 版本的 WDK，可以跳到[步骤 2:复制所选的文件](#step-2---copying-the-checked-files)。

 

在计算机上运行 32 位版本的 Windows，使用以下过程标识要复制的文件的名称：

### <a name="determining-the-name-of-the-hal-that-is-installed"></a>确定已安装的 HAL 的名称

1.  打开文件 %systemroot%\\Inf\\setupapi.dev.log 和 hal.dll 的搜索。

    您应发现如 TargetFilename 的行 hal.dll

2.  在日志文件的相同部分，查找相应*SourceFilename*。 右侧的名称*SourceFilename*需要已检验版本从中进行复制的 HAL 文件的名称。

下面的示例是从 setupapi.dev.log 文件。 *SourceFilename*是 halmacpi.dll:

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

### <a name="determining-the-name-of-the-operating-system-image-file-installed"></a>确定安装操作系统图像文件的名称

对于 64 位版本的 Windows Vista 及更高版本中，文件的名称是 ntkrnlmp.exe。

对于 32 位版本 Windows Vista，您可以使用以下过程以确定是否具有单处理器或安装的多处理器版本。

1.  在计算机管理控制台 (compmgmt.msc) 中打开事件查看器。

2.  在系统日志中找到事件 ID 6009。

    此事件的属性指示是否具有一个处理器或安装了操作系统映像的多处理器版本。

例如，下面指示带有多处理器支持的操作系统的免费版本。

```
Microsoft (R) Windows (R) 6.00. 6001 Service Pack 1 Multiprocessor Free.
```

如果您知道处理器的类型，并且在计算机上安装的物理内存量，可以从以下项之一来选择映像名称。 如果你有一个内核调试器附加，也可以使用**lmv mnt**命令来标识原始文件名。

<span id="NTOSKRNL.EXE"></span>ntoskrnl.exe  
具有 4 GB 的物理内存或更短的单处理器 x86 体系结构系统。

<span id="NTKRNLPA.EXE"></span>ntkrnlpa.exe  
PAE 支持单处理器 x86 体系结构系统。

<span id="NTKRNLMP.EXE"></span>ntkrnlmp.exe  
多处理器 x86 体系结构具有 4 GB 的物理内存或更少的系统。

<span id="NTKRPAMP.EXE"></span>ntkrpamp.exe  
PAE 支持多处理器 x86 体系结构系统。

## <a name="step-2---copying-the-checked-files"></a>步骤 2-复制所选的文件

现在，在系统安装过程中了解所使用的文件的名称，您可以将这些文件的付费版本复制到您的系统。 WDK 的调试目录中或选中的分发工具包中找到具有标识的文件。 然后将这些文件复制到 %systemroot%\\system32 目录的系统，为他们提供新的、 唯一的文件的名称。 确保文件名唯一，一种方法是重命名的文件类型从其原始的文件类型 （.dll 或.exe） 到.chk 复制时。 因此，在步骤 1 中使用的示例，你会将文件复制选中的分发工具包中，如下所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">如果是 WDK 的调试目录中的原始文件名称：</th>
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
<tr class="even">
<td align="left"><p>hal.dll</p></td>
<td align="left"><p>hal.chk</p></td>
</tr>
</tbody>
</table>

 

## <a name="step-3---changing-the-boot-parameters-using-bcdedit"></a>步骤 3-更改的启动参数，使用 BCDEdit

选中的文件复制到 %systemroot%后\\system32 目录中，必须创建一个启动时间项，使得系统以开始使用这些已检查的文件。 可以使用 BCDEdit 若要创建此。

**提示**  可以复制现有的启动项目，以创建一个新的启动项，可以修改为使用选中的操作系统映像和 HAL。 例如，若要创建的当前启动项目的副本，请使用以下命令： **bcdedit /copy {current} /d"Windows 8.1 部分检查生成"**。
有关使用 BCDEdit 的一般说明，请参阅[工具用于驱动程序测试和调试更改启动选项](boot-options-for-driver-testing-and-debugging.md)并[编辑启动选项](editing-boot-options.md)。

**请注意**  之前设置可能需要禁用或暂停 BitLocker 和安全启动的计算机上的 BCDEdit 选项。

 
若要配置部分已检验的版本，Windows Vista 及更高版本，请使用[ **BCDEdit /set** ](https://msdn.microsoft.com/library/windows/hardware/ff542202)命令并**内核**并**hal**选项。

例如，以下命令将配置为使用的内核和 HAL 付费版本的启动项。

```
bcdedit /set {44a942bf-d6ee-11e3-baf8-000ffee4f6cd} kernel ntkrnlmp.chk
```

```
bcdedit /set {44a942bf-d6ee-11e3-baf8-000ffee4f6cd} hal hal.chk
```

此外必须配置计算机以进行内核调试。 具体而言，必须启用用于启动调试的启动项目[ **BCDEdit /bootdebug**](https://msdn.microsoft.com/library/windows/hardware/ff542183)。 如果不启用启动调试并不具有内核调试程序连接到计算机，计算机将启动到 Windows 恢复环境中，如果选择此新的启动项目。

```
bcdedit /bootdebug {44a942bf-d6ee-11e3-baf8-000ffee4f6cd} on
```

若要查看命令的结果，请键入**bcdedit /enum**。 **/Enum**选项可列出所有启动项。 例如，以下启动项已修改为使用的内核和 HAL 付费版本。 您还必须启用启动的启动项目调试 (bcdedit /bootdebug {ID} 上)。

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

进行了更改，并已配置之后计算机中的内核调试，启用启动调试，并具有内核调试程序连接。 重新启动计算机。 重新启动计算机时，新的操作系统启动选项将显示，您可以选择选中的操作系统映像和 HAL。

可以使用以下过程来验证您正在运行检查生成。

1.  在计算机管理控制台 (compmgmt.msc) 中打开事件查看器。

2.  在系统日志中找到事件 ID 6009。

    此事件的属性指示是否有免费或安装了操作系统映像的内部的版本。

例如，以下说明的事件指示带有多处理器支持的操作系统已检验的版本。

```
Microsoft (R) Windows (R) 6.00. 6001 Service Pack 1 Multiprocessor Checked.
```

## <a name="related-topics"></a>相关主题


[设置调试 （内核模式和用户模式下）](https://msdn.microsoft.com/library/windows/hardware/hh450944)

[Windows 调试工具](https://msdn.microsoft.com/library/windows/hardware/ff551063)

 

 






