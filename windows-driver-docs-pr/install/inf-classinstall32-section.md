---
title: INF ClassInstall32 部分
description: ClassInstall32 部分的新类中的设备安装新的设备安装程序类 （和可能的类安装程序）。
ms.assetid: c1da44ca-3b99-43de-99ef-56fbe67b46c2
keywords:
- INF ClassInstall32 部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF ClassInstall32 Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 925d0a6d34f0d073bfc04b4dba361fd9f24cfbcf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546528"
---
# <a name="inf-classinstall32-section"></a>INF ClassInstall32 部分


**请注意**  如果要构建一个通用或移动设备的驱动程序包，此部分无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

一个**ClassInstall32**部分中安装新[设备安装程序类](device-setup-classes.md)（和可能的类安装程序） 的新类中的设备。

```ini
[ClassInstall32] | 
[ClassInstall32.nt] | 
[ClassInstall32.ntx86] |
[ClassInstall32.ntarm] | (Windows 8 and later versions of Windows) 
[ClassInstall32.ntarm64] | (Windows 10 version 1709 and later versions of Windows) 
[ClassInstall32.ntia64] | (Windows XP and later versions of Windows)
[ClassInstall32.ntamd64] (Windows XP and later versions of Windows)

AddReg=add-registry-section[,add-registry-section]...
[AddProperty=add-property-section[,add-property-section] ...]  (Windows Vista and later versions of Windows)
[Copyfiles=@filename | file-list-section[,file-list-section]...]
[DelReg=del-registry-section[,del-registry-section]...]
[DelProperty=del-property-section[,del-property-section] ...]  (Windows Vista and later versions of Windows)
[Delfiles=file-listsection[,file-list-section]...]
[Renfiles=file-list-section[,file-list-section]...]
[BitReg=bit-registry-section[,bit-registry-section]...]
[UpdateInis=update-ini-section[,update-ini-section]...]
[UpdateIniFields=update-inifields-section[,update-inifields-section]...]
[Ini2Reg=ini-to-registry-section[,ini-to-registry-section]...]
```

## <a name="entries"></a>条目


<a href="" id="addreg-add-registry-section--add-registry-section-----"></a>**AddReg=**<em>add</em>-*registry*-*section*\[**,**<em>add</em>-*registry*-*section*\] ...  
引用包含特定于类的值的条目写入到注册表的一个或多个命名的部分。 通常情况下，这用于为新的设备安装程序类提供至少一个友好名称的其他组件可以稍后从注册表中检索并使用打开这个新的设备类别，"安装"任何新的设备类安装程序和/或属性页的已安装的设备对于此设备安装程序类，其含义的提供程序。

**HKR**中任何规范*添加注册表部分*指定 **...类\\{**<em>SetupClassGUID</em>**}** 注册表项。 有关其他信息，请参阅以下**备注**部分。

有关详细信息，请参阅[ **INF AddReg 指令**](inf-addreg-directive.md)。

<a href="" id="addproperty-add-property-section--add-property-section-----"></a>**AddProperty=**<em>add-property-section</em>\[**,**<em>add-property-section</em>\] ...  
（Windows Vista 和更高版本的 Windows）引用一个或多个修改的 INF 文件部分[设备属性](device-properties.md)为设置[设备安装程序类](device-setup-classes.md)。 应使用[ **INF AddProperty 指令**](inf-addproperty-directive.md)仅可设置到 Windows Vista 或更高版本的 Windows 操作系统的新的设备安装程序类属性。

对于设备类属性，引入了之前在 Windows Server 2003、 Windows XP 或 Windows 2000 且具有对应的注册表条目值，应继续使用[ **INF AddReg 指令**](inf-addreg-directive.md)设置设备安装程序类属性。 这些准则适用于系统定义的属性和自定义属性。

有关如何使用详细信息**AddProperty**指令，请参阅[INF AddProperty 指令和 INF DelProperty 指令](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)。

<a href="" id="copyfiles--filename---file-list-section--file-list-section-----"></a>**Copyfiles = @**<em>文件名</em> | *文件*-*列表*-*部分*\[ **，**<em>文件</em>-*列表*-*部分*\] ...  
指定一个要复制到目标的源媒体中的命名的文件，或者引用一个或多个命名的部分在其中指定要传输到的目标类相关文件的源媒体上。 **DefaultDestDir**中的条目[ **DestinationDirs** ](inf-destinationdirs-section.md) INF 部分指定为任何特定于类的单个文件要复制的目标目录。

有关详细信息，请参阅[ **INF CopyFiles 指令**](inf-copyfiles-directive.md)。

**请注意**  为设备安装程序类 （和类安装程序） 的系统提供的 INF 文件不在本部分中使用此指令。

 

<a href="" id="delreg-del-registry-section--del-registry-section-----"></a>**DelReg=**<em>del</em>-*registry*-*section*\[**,**<em>del</em>-*registry*-*section*\] ...  
引用一个或多个命名指定的部分中的值的条目或密钥是在类安装程序的安装过程中从注册表中删除。

但是，如果某个特定 **{**<em>SetupClassGUID</em>**}** 子项在注册表中存在 **...类**分支，系统安装程序代码随后将忽略**ClassInstall32**指定相同的 GUID 值，以任何 INF 部分及其**版本**部分。 因此，INF 不能替换现有类安装程序或修改从其行为**ClassInstall32**部分。 若要修改现有类安装程序的行为，请使用特定于类共同安装程序。

有关详细信息，请参阅[ **INF DelReg 指令**](inf-delreg-directive.md)。

<a href="" id="delproperty-del-property-section--del-property-section-----"></a>**DelProperty=**<em>del-property-section</em>\[**,**<em>del-property-section</em>\] ...  
（Windows Vista 和更高版本的 Windows）引用一个或多个删除的 INF 文件部分[设备属性](device-properties.md)为设置[设备安装程序类](device-setup-classes.md)。 应使用[ **INF DelProperty 指令**](inf-delproperty-directive.md)只是为了删除是 Windows Vista 或更高版本的 Windows 操作系统中新增的设备安装程序类属性。

对于设备类属性，引入了之前在 Windows Server 2003、 Windows XP 或 Windows 2000 且具有对应的注册表条目值，应继续使用[ **INF DelReg 指令**](inf-delreg-directive.md)若要删除的设备安装程序类属性。 这些准则适用于系统定义的属性和自定义属性。

有关如何使用详细信息**DelProperty**指令，请参阅[INF AddProperty 指令和 INF DelProperty 指令](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)。

<a href="" id="delfiles-file-listsection--file-list-section-----"></a>**Delfiles =**<em>文件 listsection</em>\[**，**<em>文件</em>-*列表*-*一节*\] ...  
为要删除指定在其中的一个或多个命名的部分以前安装在目标上的类相关文件的引用。

有关详细信息，请参阅[ **INF DelFiles 指令**](inf-delfiles-directive.md)。

<a href="" id="renfiles-file-list-section--file-list-section-----"></a>**Renfiles =**<em>文件列表部分</em>\[**，**<em>文件</em>-*列表*-*一节*\] ...  
列出一个或多个命名的文件中的部分的相关类要重命名目标上的引用。

有关详细信息，请参阅[ **INF RenFiles 指令**](inf-renfiles-directive.md)。

<a href="" id="bitreg-bit-registry-section--bit-registry-section----"></a>**BitReg=**<em>bit-registry-section</em>\[**,**<em>bit-registry-section</em>\]...  
在本部分中有效，但几乎从不使用。

有关详细信息，请参阅[ **INF BitReg 指令**](inf-bitreg-directive.md)。

<a href="" id="updateinis-update-ini-section--update-ini-section------"></a>**UpdateInis**=*更新 ini 部分\[中，更新 ini 部分\]*...   
在本部分中有效，但几乎从不使用。

有关详细信息，请参阅[ **INF UpdateInis 指令**](inf-updateinis-directive.md)。

<a href="" id="updateinifields-update-inifields-section--update-inifields-section----"></a>**UpdateIniFields =**<em>更新 inifields 部分</em>\[**，**<em>更新 inifields 部分</em>\]...  
在本部分中有效，但几乎从不使用。

有关详细信息，请参阅[ **INF UpdateIniFields 指令**](inf-updateinifields-directive.md)。

<a href="" id="ini2reg-ini-to-registry-section--ini-to-registry-section----"></a>**Ini2Reg =**<em>注册表部分 ini</em>\[**，**<em>注册表部分 ini</em>\]...  
在本部分中有效，但几乎从不使用。

有关详细信息，请参阅[ **INF UpdateIniFields 指令**](inf-updateinifields-directive.md)。

<a name="remarks"></a>备注
-------

应包括**ClassInstall32**设备 INF 文件，只需安装新的自定义设备安装程序类中的部分。 在已安装类中，设备的 INF 文件是否[系统提供的设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff553419)或自定义类，不应包含**ClassInstall32**部分。 由于系统处理**ClassInstall32**部分，如果尚未安装一个类，则不能使用仅**ClassInstall32**部分重新安装或更改已为类设置安装。 具体而言，不能使用**ClassInstall32**部分，以添加类共同安装程序或已安装的类的类筛选器驱动程序。 有关如何安装共同安装程序和筛选器驱动程序的信息，请参阅[编写共同安装程序](writing-a-co-installer.md)并[安装筛选器驱动程序](installing-a-filter-driver.md)。

通常情况下， **ClassInstall32**部分包含一个或多个**AddReg**指令将添加在系统提供的条目*SetupClassGUID*子项在注册表中。 这些条目可以包括特定于类的"友好名称，"类安装程序路径、 类图标、 属性页提供程序，等等。

除**AddReg**和**CopyFiles**所示的其他指令，此处很少中使用**ClassInstall32**部分。

若要支持的驱动程序文件的多平台分发，构造特定于平台的**ClassInstall32**部分。 例如，所有系统安装程序 Api 都函数的过程**ClassInstall32**部分将首先搜索的**ClassInstall32.ntx86**部分 x86 平台并仅查看未修饰的**ClassInstall32**部分中找不到如果**ClassInstall32.ntx86**部分。 有关如何使用系统定义的详细信息 **.nt**， **.ntx86**， **.ntia64**， **.ntamd64**， **.ntarm**，并 **.ntarm64**扩展，请参阅[创建多个平台和操作系统的 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

**请注意**   **ClassInstall32**节名称还用于在 64 位平台上进行安装。

 

从 Windows 2000 开始，每个已安装的设备相关联[设备安装程序类](device-setup-classes.md)注册表中。 如果设备 INF 安装程序不与新的设备类安装程序，或如果其**ClassGUID =** 中的规范**版本**部分与系统定义的安装程序类 GUID，不匹配该设备的注册表子项下创建 **...类\\{**<em>UnknownClassGUID</em>**}**。

通常具有任何设备类安装程序的 INF **AddReg**指令及其**ClassInstall32**部分，若要定义至少一个命名的节创建其类型的设备的友好名称。 安装程序代码会自动创建*SetupClassGUID*中从为提供的值的注册表子项**ClassGUID =** INF 中的条目**版本**部分时安装该 （新） 的安装程序类的第一台设备。

按照本*SetupClassGUID*子项，此类 INF 还提供了的注册表信息*模型*-使用附加的特定子项**AddReg**中其指令*DDInstall*部分。 此外，INF 可以使用添加注册表部分中引用其**ClassInstall32**部分指定属性页提供程序，并对其类设备的用户界面中的处理方式进行控制。

此类特定于的类添加注册表部分具有以下常规形式：

```ini
[SetupClassAddReg]
 
HKR,,,,%DevClassName% ; device-class friendly name 
[HKR,,Installer32,,"class-installer.dll,class-entry-point"] 
[HKR,,EnumPropPages32,,"prop-provider.dll,provider-entry-point"]
HKR,,Icon,,"icon-number" 
[HKR,,SilentInstall,,1]
[HKR,,NoInstallClass,,1]
[HKR,,NoDisplayClass,,1]
```

系统使用指定的图标来表示您安装程序分发给用户。

-   如果图标值为正，它表示资源的资源标识符。 如果指定 EnumPropPages32 密钥，资源被提取从类安装程序 DLL，如果指定 Installer32 密钥，或从 DLL 中的属性页。 值"0"表示在 DLL 中的第一个图标。 保留值"1"。
-   如果图标值为负，绝对值的数值是图标的 SetupApi.DLL 中的资源标识符。

设置预定义**SilentInstall**， **NoDisplayClass**，并**NoInstallClass**类特定的注册表项中的布尔值项将产生以下影响：

-   设置 SilentInstall 指示安装程序将不弹出消息发送到用户安装的此类设备时需要响应是否随后指定 DDInstall 部分的类安装程序的 INF 文件中或在单独的 INF 文件安装的设备声明此类本身通过设置相同 ClassGuid = {ClassGUID} 规范中其各自的版本部分。 例如，CD-ROM 和磁盘设备的系统类安装程序和系统并行端口类安装程序在其各自的注册表项中设置 SilentInstall。

    如果类特定于安装程序要求安装任何设备，必须重新启动计算机，其 INF 中的特定于的类添加注册表部分不能具有此值项。

-   设置 NoDisplayClass 禁止显示此类设备管理器的所有设备的用户可见显示。 例如，打印机和网络驱动程序 （包括客户端、 服务和协议） 的系统类安装程序在其各自的注册表项中设置 NoDisplayClass。
-   设置 NoInstallClass 指示此类型的任何设备任何时候将由最终用户需要手动安装。 例如，以独占方式插 (PnP) 设备的系统类安装程序在其各自的注册表项中设置 NoInstallClass。

一个**ClassInstall32**部分可以包含**AddReg**指令设置**DeviceType**， **DeviceCharacteristics**，和**安全**适用于设备及其安装程序类。 请参阅[ **INF AddReg 指令**](inf-addreg-directive.md)有关详细信息。

<a name="examples"></a>示例
--------

此示例演示**ClassInstall32**部分中，以及名为部分它具有引用[ **AddReg 指令**](inf-addreg-directive.md)，系统 INF 显示类安装程序。

```ini
[ClassInstall32] 
AddReg=display_class_addreg

[display_class_addreg]
HKR,,,,%DisplayClassName%
HKR,,Installer32,,"Desk.Cpl,DisplayClassInstaller"
HKR,,Icon,,"-1"
```

与此相反，此示例演示在系统中 CD-ROM INF 的引用添加注册表部分**ClassInstall32**部分。 它会设置特定于类的属性页提供 CD-ROM 设备/驱动程序的安装程序。 此外会设置此 INF **SilentInstall**并**NoInstallClass**值中的 CD-ROM 类关键条目**TRUE** (**1**)。

```ini
[cdrom_class_addreg]
HKR,,,,%CDClassName%
HKR,,EnumPropPages32,,"SysSetup.Dll,CdromPropPageProvider"
HKR,,SilentInstall,,1
HKR,,NoInstallClass,,1
HKR,,Icon,,"101"
```

## <a name="see-also"></a>另请参阅


[**AddProperty**](inf-addproperty-directive.md)

[**AddReg**](inf-addreg-directive.md)

[**BitReg**](inf-bitreg-directive.md)

[**CopyFiles**](inf-copyfiles-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[**DelFiles**](inf-delfiles-directive.md)

[**DelProperty**](inf-delproperty-directive.md)

[**DelReg**](inf-delreg-directive.md)

[**Ini2Reg**](inf-ini2reg-directive.md)

[***模型***](inf-models-section.md)

[**RenFiles**](inf-renfiles-directive.md)

[**SetupDiBuildClassInfoListEx**](https://msdn.microsoft.com/library/windows/hardware/ff550911)

[**UpdateIniFields**](inf-updateinifields-directive.md)

[**UpdateInis**](inf-updateinis-directive.md)

[**版本**](inf-version-section.md)

 

 






