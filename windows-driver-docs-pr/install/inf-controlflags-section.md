---
title: INF ControlFlags 节
description: ControlFlags 节标识在安装期间 Windows 应执行特定操作的设备。
ms.assetid: 529060b6-ee4b-49a8-b723-5eda47e9f561
keywords:
- INF ControlFlags 部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF ControlFlags Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce575b5a5c70ec084843ebb322fedec7e92e08c5
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038006"
---
# <a name="inf-controlflags-section"></a>INF ControlFlags 节


**请注意**  如果你要构建通用或移动驱动程序包，此部分无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

**ControlFlags**节标识在安装期间 Windows 应执行特定操作的设备。

```ini
[ControlFlags]

ExcludeFromSelect=* | 
ExcludeFromSelect=device-identification-string[,device-identification-string] ...] | 
[ExcludeFromSelect.nt=device-identification-string[,device-identification-string] ...] | 
[ExcludeFromSelect.ntx86=device-identification-string[,device-identification-string] ...] | 
[ExcludeFromSelect.ntia64=device-identification-string[,device-identification-string] ...]  |  (Windows XP and later versions of Windows)
[ExcludeFromSelect.ntamd64=device-identification-string[,device-identification-string] ...]  |  (Windows XP and later versions of Windows)
[ExcludeFromSelect.ntarm=device-identification-string[,device-identification-string] ...]  |  (Windows XP and later versions of Windows)
[ExcludeFromSelect.ntarm64=device-identification-string[,device-identification-string] ...]  |  (Windows XP and later versions of Windows)

[CopyFilesOnly=device-identification-string[,device-identification-string] ...]
[InteractiveInstall=device-identification-string[,device-identification-string] ... ]
[RequestAdditionalSoftware=*] | 
[RequestAdditionalSoftware=device-identification-string[,device-identification-string] ...]  (Windows 7 and later versions of Windows)
```

## <a name="entries"></a>条目


<a href="" id="device-identification-string"></a>*设备标识-字符串*  
标识在 "每个制造商的[**INF 模型" 部分**](inf-models-section.md)中指定的[硬件 ID](hardware-ids.md)或[兼容 ID](compatible-ids.md) 。 每个字符串必须与下一个逗号（，）分隔。

<a href="" id="excludefromselect"></a>**ExcludeFromSelect**  
删除所有（如果指定了 \*）或从特定用户界面显示的设备的指定列表，其中用户需要从中选择特定设备进行安装。

对于 Windows 2000 和更高版本的 Windows，"查找新硬件向导" 和 "硬件更新向导" 会显示指定的设备。

若要从该显示中排除一组不兼容的操作系统或平台不兼容设备，一个或多个**ExcludeFromSelect**条目可以附加以下不区分大小写的扩展：

<a href="" id="-nt"></a> **。 nt**  
不要在运行 Windows 2000 或更高版本的 Windows 的计算机上显示这些设备。

<a href="" id="-ntx86-"></a> **. ntx86**   
不要在运行 Windows 2000 或更高版本的 Windows 的基于 x86 的计算机上显示这些设备。

<a href="" id="-ntia64--"></a> **. ntia64**   
不要在运行 Windows XP 或更高版本的 Windows 的基于 Itanium 的计算机上显示这些设备。

<a href="" id="-ntamd64"></a> **.ntamd64**  
不要在运行 Windows XP 或更高版本的 Windows 的基于 x64 的计算机上显示这些设备。

<a href="" id="-ntarm"></a> **.ntarm**  
不要在运行 Windows XP 或更高版本的 Windows 的基于 ARM 的计算机上显示这些设备。

<a href="" id="-ntarm64"></a> **.ntarm64**  
不要在运行 Windows XP 或更高版本的 Windows 的基于 ARM64 的计算机上显示这些设备。



有关如何使用**系统定义的** **ntx86**、 **ntia64**、 **ntamd64**、 **ntarm**和**Ntarm64**扩展的详细信息，请参阅[为多个平台和操作系统创建 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

<a href="" id="copyfilesonly"></a>**CopyFilesOnly**  
仅为给定设备安装 INF 指定的文件，因为设备硬件不可访问或尚未提供。

此项很少使用。 但是，它可用于预安装设备的驱动程序，该设备稍后会将其固定到当前正在使用的特定插槽中。 例如，如果需要将 INF 指定的文件传输到目标时，特定插槽中当前安装了设备，则 INF 将包含此项。

<a href="" id="interactiveinstall"></a>**InteractiveInstall**  
强制在用户的上下文中安装指定的设备列表。 每行都可以指定一个或多个硬件 Id 或兼容 Id，并且可以有一个或多个行。

此项是可选的。 安装设备的首选方法是省略此项，并允许 Windows 在受信任的系统线程的上下文中安装设备（如果可能）。 但是，如果设备在安装设备时确实要求用户登录，请在设备 INF 中包含此项。

<a href="" id="requestadditionalsoftware"></a>**RequestAdditionalSoftware**  
指定所有（如果指定了 **\*** ）或指定的设备列表可能需要比通过设备的[驱动程序包](driver-packages.md)安装的软件更多的软件。 例如， **RequestAdditionalSoftware**项可用于安装驱动程序包中未包含的新的或更新的特定于设备的软件。

**注意** 如果未指定 **\*** ，则必须在 " [**INF 模型" 部分**](inf-models-section.md)中定义**RequestAdditionalSoftware**条目指定的每个设备。

 

此项是可选的，在 windows 7 及更高版本的 Windows 操作系统中受支持。

Windows 安装设备的[驱动程序包](driver-packages.md)后，如果在 INF 文件中指定**RequestAdditionalSoftware**项，即插即用（PnP）管理器将执行以下步骤：

1.  PnP 管理器使用**RequestAddtionalSoftware**类型生成问题报告和解决方案（pr）错误报告。 此报表包含有关设备的特定硬件 ID 和计算机的系统体系结构的信息。
2.  如果有独立硬件供应商（IHV）提供的用于特定于设备的软件的解决方案，则该解决方案将下载到计算机。

    **请注意**  下载解决方案不会安装软件本身。

     

3.  如果计算机上未安装特定于设备的软件，则 PnP 管理器向用户显示解决方案，并提供下载软件的链接。 然后，用户可以根据解决方案中提供的说明，选择下载并安装此软件。

<a name="remarks"></a>备注
-------

通常， **ControlFlags**节有一个或多个**ExcludeFromSelect**条目用于标识 "每个制造商的[**INF 模型" 部分**](inf-models-section.md)中列出的设备，但不应在手动安装过程中将其作为选项显示给最终用户。

在**ExcludeFromSelect**项中列出设备的[硬件 ID](hardware-ids.md)或[兼容 ID](compatible-ids.md)会将其从显示给最终用户的显示中移除。 如果为**ExcludeFromSelect**值指定星号（\*），将从此用户可见列表中删除 INF 文件中定义的所有设备/模型。

INF 编写器应慎用并仅在以下情况下使用**InteractiveInstall**指令：

-   为已损坏或错误定义了硬件 Id 的设备安装驱动程序。 例如，当两个或多个不同的设备共享相同的硬件 ID 时。 即插即用标准严格禁止这种情况，但一些硬件供应商在硬件中发生了此错误。
-   为需要其自己的驱动程序的设备安装驱动程序，并且绝对不能使用泛型类驱动程序或操作系统提供的另一个驱动程序。 **InteractiveInstall**项强制设备管理器要求用户确认兼容 ID 匹配。

**请注意**  将来，WHQL 可能不会向其 INF 文件包含**InteractiveInstall**条目的设备授予 Windows 徽标。

 

仅安装 PnP 设备的 INF 文件可以具有**ControlFlags**部分，除非它们将其各自*SetupClassGUID*注册表项中的**NoInstallClass**值项设置为**TRUE**。 有关这些注册表项的详细信息，请参阅[**INF ClassInstall32 部分**](inf-classinstall32-section.md)。

<a name="examples"></a>示例
--------

System 老鼠类安装程序 INF 中**ControlFlags**部分的此示例将禁止显示无法安装在 x86 平台上的设备/型号。

```ini
[ControlFlags]
; Exclude all bus mice and InPort mice for x86 platforms
ExcludeFromSelect.ntx86=*PNP0F0D,*PNP0F11,*PNP0F00,*PNP0F02,*PNP0F15
; Hide this entry always
ExcludeFromSelect=UNKNOWN_MOUSE
```

以下 INF 文件片段显示两个设备：一个完全支持 PnP 且在安装过程中不需要用户干预，另一个需要其自己的驱动程序，也不能使用其他任何驱动程序。 为第二个设备指定**InteractiveInstall**将强制 Windows 在用户的上下文（具有管理权限的用户）中安装该设备。 这包括根据需要提示用户提供驱动程序文件（INF 文件、驱动程序文件等）的位置。

```ini
; ...
[Manufacturer]
%Mfg% = ModelsSection

[ModelsSection]
; Models section, with two entries
%Device1.DeviceDesc% = Device1.Install, \
    PCI\VEN_1000&DEV_0001&SUBSYS_00000000&REV_01
%Device2.Device.Desc%= Device2.Install, \
    PCI\VEN_1000&DEV_0001&SUBSYS_00000000&REV_02

[ControlFlags]
InteractiveInstall = \
  PCI\VEN_1000&DEV_0001&SUBSYS_00000000&REV_02
; ...
```

## <a name="see-also"></a>另请参阅


[**ClassInstall32**](inf-classinstall32-section.md)

[**提供**](inf-manufacturer-section.md)

[***机型***](inf-models-section.md)

 

 






