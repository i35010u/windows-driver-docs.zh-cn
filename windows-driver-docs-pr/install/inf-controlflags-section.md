---
title: INF ControlFlags Section
description: ControlFlags 部分标识为其 Windows 应采取某些唯一在安装过程中的设备。
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
ms.openlocfilehash: 3f52af6a0d8677d494ec80d865041c326ba3a6f4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522504"
---
# <a name="inf-controlflags-section"></a>INF ControlFlags Section


**请注意**  如果要构建一个通用或移动设备的驱动程序包，此部分无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

一个**ControlFlags**部分标识为其 Windows 应采取某些唯一在安装过程中的设备。

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


<a href="" id="device-identification-string"></a>*device-identification-string*  
标识[硬件 ID](hardware-ids.md)或[兼容 ID](compatible-ids.md)指定在每个制造商[ **INF 模型部分**](inf-models-section.md)。 必须用逗号 （，） 分隔每个字符串。

<a href="" id="excludefromselect"></a>**ExcludeFromSelect**  
移除所有 (如果\*指定) 或指定来自特定用户界面显示，从其预期用户可以选择安装一个特定设备的设备的列表。

对于 Windows 2000 和更高版本的 Windows 中，指定的设备会显示通过发现新硬件向导和硬件更新向导。

若要排除此显示中，一个或多个在一组不兼容的操作系统或平台不兼容的设备**ExcludeFromSelect**条目可以是追加了以下不区分大小写扩展：

<a href="" id="-nt"></a>**.nt**  
不会显示这些设备上运行的 Windows 2000 或更高版本的 Windows 的计算机。

<a href="" id="-ntx86-"></a>**.ntx86**   
不会显示这些设备上运行的 Windows 2000 或更高版本的 Windows 的基于 x86 的计算机。

<a href="" id="-ntia64--"></a>**.ntia64**   
不会显示这些设备上运行的 Windows XP 或更高版本的 Windows 的基于 Itanium 的计算机。

<a href="" id="-ntamd64"></a>**.ntamd64**  
不会显示这些设备上运行的 Windows XP 或更高版本的 Windows 的基于 x64 的计算机。

<a href="" id="-ntarm"></a>**.ntarm**  
运行 Windows XP 或更高版本的 Windows 的基于 ARM 的计算机上不显示这些设备。

<a href="" id="-ntarm64"></a>**.ntarm64**  
运行 Windows XP 或更高版本的 Windows 的基于 ARM64 的计算机上不显示这些设备。



有关如何使用系统定义的详细信息 **.nt**， **.ntx86**， **.ntia64**， **.ntamd64**， **.ntarm**，并 **.ntarm64**扩展，请参阅[创建多个平台和操作系统的 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

<a href="" id="copyfilesonly"></a>**CopyFilesOnly**  
安装适用于给定设备仅 INF 指定的文件，因为设备硬件尚不可访问或可用。

很少使用此项。 但是，它可以用于预安装为其卡将更高版本安装在当前正在使用的特定位置的设备的驱动程序。 例如，如果当前被安装在特定位置的设备有必要将 INF 指定文件传输到目标，INF 必须此项。

<a href="" id="interactiveinstall"></a>**InteractiveInstall**  
强制指定的用户的上下文中安装的设备列表。 每个行可以指定一个或多个硬件 Id 或兼容 Id，并可以有一个或多个行。

此项是可选的。 安装设备的首选的方法是以忽略此项，并允许 Windows 在可能的情况的受信任的系统线程上下文中安装该设备。 但是，如果设备绝对需要登录的用户安装时的设备，设备 INF 中包括此项。

<a href="" id="requestadditionalsoftware"></a>**RequestAdditionalSoftware**  
指定的所有 (如果**\\*** 指定) 或指定的设备列表可能需要比什么通过安装其他软件[驱动程序包](driver-packages.md)设备。 例如， **RequestAdditionalSoftware**条目可以用来安装新的或更新驱动程序包中未包括的特定于设备的软件。

**请注意**如果**\\*** 未指定，则通过指定每个设备**RequestAdditionalSoftware**内必须定义入口[ **INF模型部分**](inf-models-section.md)。

 

此条目是可选的并支持 Windows 7 和更高版本的 Windows 操作系统中。

Windows 安装后[驱动程序包](driver-packages.md)对于设备，插即用 (PnP) 管理器执行以下步骤，如果**RequestAdditionalSoftware** INF 文件中指定条目：

1.  PnP 管理器的类型生成问题报告和解决方案 (PR) 的错误报告**RequestAddtionalSoftware**。 此报表包含有关特定的硬件 ID 的设备和计算机的系统体系结构的信息。
2.  如果有由独立硬件供应商 (IHV) 提供特定于设备的软件的解决方案，则将解决方案下载到计算机。

    **请注意**  下载该解决方案不会安装软件本身。

     

3.  如果在计算机上未安装特定于设备的软件，即插即用管理器将该解决方案显示给用户和下载该软件提供的链接。 然后，用户可以选择下载并安装此软件提供解决方案中的说明。

<a name="remarks"></a>备注
-------

通常情况下， **ControlFlags**部分包含一个或多个**ExcludeFromSelect**条目来标识每个制造商中列出的设备[ **INF 模型部分**](inf-models-section.md)，但这不应显示给最终用户的选项在手动安装过程。

列出的设备[硬件 ID](hardware-ids.md)或[兼容 ID](compatible-ids.md)中**ExcludeFromSelect**条目将其从显示给最终用户删除。 指定星号 (\*) 用于**ExcludeFromSelect**值中删除此用户可见的列表中的 INF 文件中定义的所有设备/模型。

INF 编写器应使用**InteractiveInstall**指令尽量少以及仅在以下情况下：

-   若要安装的已损坏或否则未正确定义的硬件 Id 的设备驱动程序。 例如，当两个或多个不同的设备共享相同的硬件 id。 这种情况下被严格禁止 Plug and play 标准，但有些硬件供应商在硬件中进行此错误。
-   若要安装的需要其自己的驱动程序，并且绝对不能使用泛型类驱动程序或提供的另一个驱动程序与操作系统的设备驱动程序。 **InteractiveInstall**项强制要求用户确认兼容 id 匹配的设备管理器。

**请注意**  WHQL 可能在将来，授予到设备的 INF 文件包含 Windows 徽标**InteractiveInstall**条目。

 

以独占方式安装即插即用设备的 INF 文件可以具有**ControlFlags**部分，除非这些设置，否则**NoInstallClass**值在其各自项目*SetupClassGUID*注册表项向 **，则返回 TRUE**。 有关这些注册表项的详细信息，请参阅[ **INF ClassInstall32 部分**](inf-classinstall32-section.md)。

<a name="examples"></a>示例
--------

此示例中的**ControlFlags**部分系统鼠标类安装程序 INF 中的禁止显示的设备/模型不能安装在 x86 上的平台。

```ini
[ControlFlags]
; Exclude all bus mice and InPort mice for x86 platforms
ExcludeFromSelect.ntx86=*PNP0F0D,*PNP0F11,*PNP0F00,*PNP0F02,*PNP0F15
; Hide this entry always
ExcludeFromSelect=UNKNOWN_MOUSE
```

下面的 INF 文件片断演示两个设备： 一个用于完全 PnP 支持并无需用户干预期间安装，另一个需要其自己的驱动程序，并且不能使用任何其他驱动程序。 指定**InteractiveInstall**第二个设备会强制 Windows 用户的上下文 （具有管理权限的用户） 中安装此设备。 这包括提示用户输入所需的驱动程序文件 （INF 文件、 驱动程序文件等） 的位置。

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

[**制造商**](inf-manufacturer-section.md)

[***模型***](inf-models-section.md)

 

 






