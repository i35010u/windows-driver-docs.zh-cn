---
title: INF ClassInstall32 节
description: ClassInstall32 节 (安装新的设备安装程序类，并可能为新类中的设备安装类安装程序) 。
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
ms.openlocfilehash: 400165d2f8884690bcb2cf3fc6204ea56321a738
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716182"
---
# <a name="inf-classinstall32-section"></a>INF ClassInstall32 节


**注意**   如果要构建通用或移动驱动程序包，此部分无效。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

**ClassInstall32**节 (安装新的[设备安装程序类](./overview-of-device-setup-classes.md)，并可能为新类中的设备安装类安装程序) 。

```inf
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

## <a name="entries"></a>项


<a href="" id="addreg-add-registry-section--add-registry-section-----"></a>**AddReg =**<em>添加</em> - *注册表* - *部分* \[ **，**<em>添加</em> - *注册表* - *部分* \] .。。  
引用一个或多个命名节，其中包含要写入注册表中的特定于类的值项。 通常，此名称用于至少为新设备安装程序类提供一个友好名称，其他组件以后可以从注册表中检索该名称，并使用此名称打开此新设备类的已安装设备，以便 "安装" 此设备安装程序类的任何新设备类安装程序和/或属性页提供程序等。

任何 "*添加注册表" 一节*中的**HKR**规范都指定 **。类 \\ {**<em>SetupClassGUID</em>**}** 注册表项。 有关其他信息，请参阅下面的 " **备注** " 部分。

有关详细信息，请参阅 [**INF AddReg 指令**](inf-addreg-directive.md)。

<a href="" id="addproperty-add-property-section--add-property-section-----"></a>**AddProperty =**<em>添加属性</em>-节 \[ **，**<em>添加属性-节</em> \] .。。  
 (Windows Vista 和更高版本的 Windows) 引用一个或多个 INF 文件部分，这些部分修改为[设备安装程序类](./overview-of-device-setup-classes.md)设置的[设备属性](device-properties.md)。 只应使用 [**INF AddProperty 指令**](inf-addproperty-directive.md) 设置 windows Vista 或更高版本的 windows 操作系统的新设备安装程序类属性。

对于之前在 Windows Server 2003、Windows XP 或 Windows 2000 上引入的设备类属性以及具有相应注册表项值的设备类属性，应继续使用 [**INF AddReg 指令**](inf-addreg-directive.md) 设置设备安装程序类属性。 这些准则适用于系统定义的属性和自定义属性。

有关如何使用 **AddProperty** 指令的详细信息，请参阅 [使用 inf ADDPROPERTY 指令和 inf DelProperty 指令](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)。

<a href="" id="copyfiles--filename---file-list-section--file-list-section-----"></a>**Copyfiles = @**<em>filename</em>  |  *file* - *list* - *部分* \[ **，**<em>file</em> - *list* - *节* \] .。。  
指定一个或多个命名节，将源媒体中的一个或多个已命名的文件复制到目标，或引用一个或多个命名节，其中源媒体上的类相关文件将被指定为传输到目标。 INF 的[**DestinationDirs**](inf-destinationdirs-section.md)部分中的**DefaultDestDir**条目指定要复制的任何特定于类的单个文件的目标目录。

有关详细信息，请参阅 [**INF CopyFiles 指令**](inf-copyfiles-directive.md)。

**注意**   系统提供的设备安装程序类 (和类安装程序的 INF 文件) 在此部分中不要使用此指令。

 

<a href="" id="delreg-del-registry-section--del-registry-section-----"></a>**DelReg =**<em>del</em> - *registry* - *部分* \[ **，**<em>del</em> - *registry* - *部分* \] .。。  
引用一个或多个命名节，其中指定了在安装类安装程序的过程中要从注册表删除值项或键。

但是，如果注册表中存在特定的 **{**<em>SetupClassGUID</em>**}** 子项，则为 **。类**分支中，系统设置代码随后会忽略在其**版本**部分中指定同一 GUID 值的任何 INF 的**ClassInstall32**部分。 因此，INF 无法替换现有的类安装程序或从 **ClassInstall32** 节修改其行为。 若要修改现有类安装程序的行为，请使用特定于类的共同安装程序。

有关详细信息，请参阅 [**INF DelReg 指令**](inf-delreg-directive.md)。

<a href="" id="delproperty-del-property-section--del-property-section-----"></a>**DelProperty =**<em>del-property 节</em> \[ **，**<em>del</em> \] .。。  
 (Windows Vista 和更高版本的 Windows) 引用一个或多个 INF 文件部分，这些部分将删除为[设备安装程序类](./overview-of-device-setup-classes.md)设置的[设备属性](device-properties.md)。 只应使用 [**INF DelProperty 指令**](inf-delproperty-directive.md) 来删除 windows Vista 或更高版本的 windows 操作系统的新设备安装程序类属性。

对于之前在 Windows Server 2003、Windows XP 或 Windows 2000 上引入的设备类属性以及具有相应注册表项值的设备类属性，应继续使用 [**INF DelReg 指令**](inf-delreg-directive.md) 删除设备安装程序类属性。 这些准则适用于系统定义的属性和自定义属性。

有关如何使用 **DelProperty** 指令的详细信息，请参阅 [使用 inf ADDPROPERTY 指令和 inf DelProperty 指令](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)。

<a href="" id="delfiles-file-listsection--file-list-section-----"></a>**Delfiles =**<em>listsection</em> \[ **，**<em>file</em> - *list* - *节* \] .。。  
引用一个或多个命名节，其中先前在目标上安装的与类相关的文件将被指定为删除。

有关详细信息，请参阅 [**INF DelFiles 指令**](inf-delfiles-directive.md)。

<a href="" id="renfiles-file-list-section--file-list-section-----"></a>**Renfiles =**<em>文件</em>列表节 \[ **，**<em>文件</em> - *列表* - *节* \] .。。  
引用一个或多个命名节，其中列出了要在目标上重命名的类相关文件。

有关详细信息，请参阅 [**INF RenFiles 指令**](inf-renfiles-directive.md)。

<a href="" id="bitreg-bit-registry-section--bit-registry-section----"></a>**BitReg =**<em>位注册表-节</em> \[ **，**<em>位注册表-节</em> \] .。。  
在此部分有效，但几乎从未使用过。

有关详细信息，请参阅 [**INF BitReg 指令**](inf-bitreg-directive.md)。

<a href="" id="updateinis-update-ini-section--update-ini-section------"></a>**UpdateInis** =*更新-ini-节 \[ ，更新-ini-节 \] *.。。   
在此部分有效，但几乎从未使用过。

有关详细信息，请参阅 [**INF UpdateInis 指令**](inf-updateinis-directive.md)。

<a href="" id="updateinifields-update-inifields-section--update-inifields-section----"></a>**UpdateIniFields =**<em>inifields-section</em> \[ **，**<em>inifields-节</em> \] .。。  
在此部分有效，但几乎从未使用过。

有关详细信息，请参阅 [**INF UpdateIniFields 指令**](inf-updateinifields-directive.md)。

<a href="" id="ini2reg-ini-to-registry-section--ini-to-registry-section----"></a>**Ini2Reg =**<em>ini 到注册表-节</em> \[ **，**<em>ini 到注册表-节</em> \] .。。  
在此部分有效，但几乎从未使用过。

有关详细信息，请参阅 [**INF UpdateIniFields 指令**](inf-updateinifields-directive.md)。

<a name="remarks"></a>备注
-------

只应在设备 INF 文件中包含一个 **ClassInstall32** 部分，以安装新的自定义设备安装程序类。 已安装类中的设备的 INF 文件，无论 [系统提供的设备安装程序类](/previous-versions/ff553419(v=vs.85)) 还是自定义类，都不应包含 **ClassInstall32** 部分。 由于系统仅当尚未安装类时才处理 **ClassInstall32** 部分，因此不能使用 **ClassInstall32** 部分来重新安装或更改已安装的类的设置。 特别是，不能使用 **ClassInstall32** 部分为已安装的类添加类联安装程序或类筛选器驱动程序。 有关如何安装共同安装程序和筛选器驱动程序的信息，请参阅 [编写共同安装](writing-a-co-installer.md) 程序和 [安装筛选器驱动程序](installing-a-filter-driver.md)。

通常， **ClassInstall32** 节包含一个或多个 **AddReg** 指令，可在注册表中系统提供的 *SetupClassGUID* 子项下添加条目。 这些项可以包括特定于类的 "友好名称"、"类安装程序路径"、"类图标"、"属性页提供程序" 等。

除了 **AddReg** 和 **CopyFiles**，此处所示的其他指令很少用于 **ClassInstall32** 部分。

若要支持驱动程序文件的多平台分发，请构造特定于平台的 **ClassInstall32** 部分。 例如，处理 **ClassInstall32** 部分的所有系统 setupapi.log 函数将首先搜索 x86 平台上的 **ClassInstall32** 节，并仅检查未修饰的 **ClassInstall32** 部分（如果它们找不到 **ClassInstall32** 节）。 有关如何使用 **系统定义的** **ntx86**、 **ntia64**、 **ntamd64**、 **ntarm**和 **Ntarm64** 扩展的详细信息，请参阅 [为多个平台和操作系统创建 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

**注意**   **ClassInstall32**节名称还用于64位平台上的安装。

 

从 Windows 2000 开始，每个已安装的设备都与注册表中的 [设备安装程序类](./overview-of-device-setup-classes.md) 相关联。 如果要安装的设备的 INF 未与新的设备类安装程序相关联，或者其 **ClassGUID =** **规范与系统** 定义的安装程序类 GUID 不匹配，则将在下创建该设备的注册表 **子项。类 \\ {**<em>UnknownClassGUID</em>**}**。

任何设备类安装程序的 INF 通常在其**ClassInstall32**部分中都有一个**AddReg**指令，以便定义至少一个命名节，该节为其设备类型创建友好名称。 当安装 (新的) 安装程序类的第一个设备时，安装代码会在注册表中自动从为 INF 的 "**版本**" 部分中的**ClassGUID =** 条目提供的值创建一个*SetupClassGUID*子项。

在此*SetupClassGUID*子项下，此类 INF 还会通过在其*DDInstall*节中使用其他**AddReg**指令来提供特定于*模型*的子项的注册表信息。 此外，INF 可以使用其 **ClassInstall32** 部分中引用的 "添加注册表" 部分来指定属性页提供程序，并控制其设备类在用户界面中的处理方式。

此类特定的 "添加注册表" 部分具有以下常规形式：

```inf
[SetupClassAddReg]
 
HKR,,,,%DevClassName% ; device-class friendly name 
[HKR,,Installer32,,"class-installer.dll,class-entry-point"] 
[HKR,,EnumPropPages32,,"prop-provider.dll,provider-entry-point"]
HKR,,Icon,,"icon-number" 
[HKR,,SilentInstall,,1]
[HKR,,NoInstallClass,,1]
[HKR,,NoDisplayClass,,1]
```

系统使用指定的图标来向用户显示您的安装程序。

-   如果图标值为正值，则表示资源的资源标识符。 如果指定了 Installer32 键，则从类安装程序 DLL 提取资源，如果指定了 EnumPropPages32 键，则从属性页 DLL 提取资源。 值 "0" 表示 DLL 中的第一个图标。 值 "1" 为保留值。
-   如果图标值为负数，则绝对值是 SetupApi.DLL 中的图标的资源标识符。

在特定于类的注册表项中设置预定义的 **SilentInstall**、 **NoDisplayClass**和 **NoInstallClass** 布尔值项具有以下效果：

-   设置 SilentInstall 指导安装程序在安装此类的设备时向用户发送无弹出消息，此类消息需要响应，无论是在类安装程序的 INF 文件的 DDInstall 部分中指定，还是在单独的 INF 文件中，通过在其各自版本部分中设置相同的 ClassGuid = {ClassGUID} 规范来声明该类。 例如，cd-rom 和磁盘设备的系统类安装程序以及系统并行端口类安装程序将 SilentInstall 设置为其各自的注册表项。

    如果特定于类的安装程序要求对它安装的任何设备重新启动计算机，则其 INF 中特定于类的 "添加注册表" 部分不能有此值条目。

-   设置 NoDisplayClass 通过设备管理器取消显示此类的所有设备的用户可见的显示。 例如，用于打印机和网络驱动程序的系统类安装程序 (包括客户端、服务和协议) 在其各自的注册表项中设置 NoDisplayClass。
-   设置 NoInstallClass 表示此类型的任何设备都不需要由最终用户手动安装。 例如，以独占方式即插即用的系统类安装程序 (PnP) 设备在各自的注册表项中设置 NoInstallClass。

**ClassInstall32**节可以包含**AddReg**指令，以设置其安装程序类的设备的**DeviceType**、 **DeviceCharacteristics**和**Security** 。 有关详细信息，请参阅 [**INF AddReg 指令**](inf-addreg-directive.md) 。

<a name="examples"></a>示例
--------

此示例显示了 **ClassInstall32** 节以及它引用的命名节，其中包含系统显示类安装程序 INF 的 [**AddReg 指令**](inf-addreg-directive.md)。

```inf
[ClassInstall32] 
AddReg=display_class_addreg

[display_class_addreg]
HKR,,,,%DisplayClassName%
HKR,,Installer32,,"Desk.Cpl,DisplayClassInstaller"
HKR,,Icon,,"-1"
```

与此相反，此示例显示了在系统 CD-ROM INF 的 **ClassInstall32** 部分中引用的 "添加注册表" 部分。 它为安装的 CD-ROM 设备/驱动程序设置特定于类的属性页提供程序。 此 INF 还将 CD-ROM 类键中的 **SilentInstall** 和 **NoInstallClass** 值项设置为 **TRUE** (**1**) 。

```inf
[cdrom_class_addreg]
HKR,,,,%CDClassName%
HKR,,EnumPropPages32,,"SysSetup.Dll,CdromPropPageProvider"
HKR,,SilentInstall,,1
HKR,,NoInstallClass,,1
HKR,,Icon,,"101"
```

## <a name="see-also"></a>请参阅


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

[**SetupDiBuildClassInfoListEx**](/windows/win32/api/setupapi/nf-setupapi-setupdibuildclassinfolistexa)

[**UpdateIniFields**](inf-updateinifields-directive.md)

[**UpdateInis**](inf-updateinis-directive.md)

[**版本**](inf-version-section.md)

 

