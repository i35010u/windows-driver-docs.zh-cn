---
title: INF DDInstall 节
description: 每个每个模型 DDInstall 部分包含一个可选的 DriverVer 指令和一个或多个指令引用 copyfiles 部分和 AddReg，最常指定 INF 指令与此处显示的 INF 文件中的其他命名的部分首先列出。
ms.assetid: 79cba88d-fda1-4b91-bf51-98afd7224bc9
keywords:
- INF DDInstall 部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF DDInstall Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bc7a950388bd1df089d54046b600d9d45cffa0c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566694"
---
# <a name="inf-ddinstall-section"></a>INF DDInstall 节


每个每个模型*DDInstall*一节包含一个可选**DriverVer**指令和一个或多个指令引用其他命名 INF 文件中的部分使用的最大频率如下所示指定 INF 指令**CopyFiles**并**AddReg**，首先列出。

这些指令引用的各节包含有关安装驱动程序文件和任何特定于设备的和/或特定于驱动程序的信息写入注册表的说明。

```ini
[install-section-name] | 
[install-section-name.nt] | 
[install-section-name.ntx86] | 
[install-section-name.ntia64] |  (Windows XP and later versions of Windows)
[install-section-name.ntamd64]  (Windows XP and later versions of Windows)

[DriverVer=mm/dd/yyyy[,x.y.v.z] ]
[CopyFiles=@filename | file-list-section[,file-list-section] ...]
[CopyINF=filename1.inf[,filename2.inf]...]   (Windows XP and later versions of Windows)
[AddReg=add-registry-section[,add-registry-section]...]
[AddProperty=add-registry-section[,add-registry-section]...]  (Windows Vista and later versions of Windows)
[Include=filename1.inf[,filename2.inf]...]
[Needs=inf-section-name[,inf-section-name]...]
[Delfiles=file-list-section[,file-list-section]...]
[Renfiles=file-list-section[,file-list-section]...]
[DelReg=del-registry-section[,del-registry-section]...]
[DelProperty=add-registry-section[,add-registry-section]...]  (Windows Vista and later versions of Windows)
[FeatureScore=featurescore]...  (Windows Vista and later versions of Windows)
[BitReg=bit-registry-section[,bit-registry-section]...]
[LogConfig=log-config-section[,log-config-section]...]
[ProfileItems=profile-items-section[,profile-items-section]...]  (Microsoft Windows 2000 and later versions of Windows)
[UpdateInis=update-ini-section[,update-ini-section]...]
[UpdateIniFields=update-inifields-section[,update-inifields-section]...]
[Ini2Reg=ini-to-registry-section[,ini-to-registry-section]...]
[RegisterDlls=register-dll-section[,register-dll-section]...]
[UnregisterDlls=unregister-dll-section[,unregister-dll-section]...]
[ExcludeID=device-identification-string[,device-identification-string]...]...  ((Windows XP and later versions of Windows)
[Reboot]
```

## <a name="entries"></a>条目


<a href="" id="driverver-mm-dd-yyyy--x-y-v-z--"></a>**DriverVer=**<em>mm/dd/yyyy</em>\[**,**<em>x.y.v.z</em>\]   
此可选条目指定的版本信息[驱动程序包](driver-packages.md)。

有关如何指定此项的信息，请参阅[ **INF DriverVer 指令**](inf-driverver-directive.md)。

<a href="" id="copyfiles--filename---file-list-section--file-list-section-----"></a>**CopyFiles = @**<em>文件名</em> | *文件列表部分*\[**，**<em>文件列表节</em>\] ...  
此指令指定一个要复制到目标的源媒体中的命名的文件，或者引用一个或多个 INF 编写器定义的节在其中指定要传输到目标设备相关文件的源媒体上。 **CopyFiles**指令是可选的但在大多数存在*DDInstall*部分。

**DefaultDestDir**中的条目[ **DestinationDirs** ](inf-destinationdirs-section.md) INF 部分指定任何单个文件要复制的目标。 [ **SourceDisksNames** ](inf-sourcedisksnames-section.md)并[ **SourceDisksFiles** ](inf-sourcedisksfiles-section.md)部分中或其他 INF 中指定**LayoutFile**条目的此 INF [**版本**](inf-version-section.md)部分中，驱动程序文件在分发媒体提供的位置。

有关详细信息，请参阅[ **INF CopyFiles 指令**](inf-copyfiles-directive.md)。

<a href="" id="copyinf-filename1-inf--filename2-inf----"></a>**CopyINF=**<em>filename1</em>**.inf**\[**,**<em>filename2</em>**.inf**\]...  
(Windows XP 及更高版本)此指令会导致指定的 INF 文件复制到目标系统。

有关详细信息，请参阅[ **INF CopyINF 指令**](inf-copyinf-directive.md)。

<a href="" id="addreg-add-registry-section--add-registry-section----"></a>**AddReg=**<em>add-registry-section</em>\[**,**<em>add-registry-section</em>\]...  
此指令引用一个或多个 INF 编写器定义指定的部分中的新子项，也可能包含初始值的条目，是要写入到注册表或中的现有密钥值项进行修改。

**HKR**中此类添加注册表部分规范指定 **...类\\**<em>SetupClassGUID</em>**\\**<em>设备实例 id</em>用户可访问驱动程序的注册表路径。 这种类型的**HKR**规范也称为。 "软件密钥"。

有关详细信息，请参阅[ **INF AddReg 指令**](inf-addreg-directive.md)。

<a href="" id="addproperty-add-registry-section--add-registry-section----"></a>**AddProperty =**<em>添加注册表部分</em>\[**，**<em>添加注册表部分</em>\]...  
(Windows Vista 及更高版本)引用一个或多个修改的 INF 文件部分[设备属性](device-properties.md)设备实例设置。 应使用[ **INF AddProperty 指令**](inf-addproperty-directive.md)仅可设置到 Windows Vista 或更高版本的 Windows 操作系统的新的设备实例属性。

对于设备实例属性，引入了之前在 Windows Server 2003、 Windows XP 或 Windows 2000 且具有对应的注册表条目值，应继续使用[ **INF AddReg 指令**](inf-addreg-directive.md)设置实例属性的设备。 这些准则适用于系统定义的属性和自定义属性。 有关如何使用详细信息**AddProperty**指令，请参阅[INF AddProperty 指令和 INF DelProperty 指令](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)。

<a href="" id="include-filename1-inf--filename2-inf----"></a>**Include=**<em>filename1</em>**.inf**\[**,**<em>filename2</em>**.inf**\]...  
此可选项指定一个或多个其他系统提供 INF 文件包含安装此设备和/或驱动程序所需的部分。 如果指定此项时，通常那么**需要**条目。

例如，依赖于系统的内核流支持的设备驱动程序的系统 INF 文件指定了该条目，如下所示：

```ini
Include= ks.inf[, [kscaptur.inf,] [ksfilter.inf]]...
```

有关详细信息**Include**条目和限制其使用时，请参阅[设备文件中指定的源和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**需要 =**<em>inf 部分名称</em>\[**，**<em>inf 部分名称</em>\]...  
此可选项指定必须在此设备的安装过程中处理的系统提供 INF 文件内的部分。 通常情况下，此类指定的部分是*DDInstall* (或<em>DDInstall</em>**。**<em>xxx</em>) 部分中所示的 INF 文件之一**Include**条目。 但是，它可以是任何部分此类中被引用*DDInstall*或<em>DDInstall</em>**。**<em>xxx</em>包含 INF 部分。

例如，已在前面的设备驱动程序的 INF 文件**Include**条目指定了该条目，如下所示：

```ini
Needs= KS.Registration[, KSCAPTUR.Registration | KSCAPTUR.Registration.NT, MSPCLOCK.Installation]
```

**需要**条目不能嵌套。 有关详细信息**需要**条目和限制其使用时，请参阅[设备文件中指定的源和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a href="" id="delfiles-file-list-section--file-list-section----"></a>**Delfiles =**<em>文件列表部分</em>\[**，**<em>文件列表部分</em>\]...  
此指令引用一个或多个 INF 编写器定义部分列出要删除在目标上的文件。

有关详细信息，请参阅[ **INF DelFiles 指令**](inf-delfiles-directive.md)。

<a href="" id="renfiles-file-list-section--file-list-section----"></a>**Renfiles =**<em>文件列表部分</em>\[**，**<em>文件列表部分</em>\]...  
此指令引用一个或多个 INF 编写器定义部分列出要重命名目标上之前设备相关的源代码文件复制到目标计算机的文件。

有关详细信息，请参阅[**INF RenFiles 指令**](inf-renfiles-directive.md)。

<a href="" id="delreg-del-registry-section--del-registry-section----"></a>**DelReg=**<em>del-registry-section</em>\[**,**<em>del-registry-section</em>\]...  
此指令引用一个或多个 INF 编写器定义指定的部分中的密钥和/或值的条目是在设备的安装过程中从注册表中删除。

通常情况下，此指令用于处理升级时 INF 必须清理旧的注册表条目从以前安装的此设备。

**HKR**规范中删除注册表部分指定 **...类\\**<em>SetupClassGUID</em>**\\**<em>设备实例 id</em>用户可访问驱动程序的注册表路径。 这种类型的**HKR**规范也称为。 "软件密钥"。

有关详细信息，请参阅[ **INF DelReg 指令**](inf-delreg-directive.md)。

<a href="" id="delproperty-add-registry-section--add-registry-section----"></a>**DelProperty =**<em>添加注册表部分</em>\[**，**<em>添加注册表部分</em>\]...  
(Windows Vista 及更高版本)引用一个或多个删除的 INF 文件部分[设备属性](device-properties.md)设备实例设置。 应使用[ **INF DelProperty 指令**](inf-delproperty-directive.md)仅要删除设备实例属性的新 Windows Vista 或更高版本的 Windows。

对于设备实例属性，引入了之前在 Windows Server 2003、 Windows XP 或 Windows 2000 且具有对应的注册表条目值，应继续使用[ **INF DelReg 指令**](inf-delreg-directive.md)若要删除设备实例属性。 这些准则适用于系统定义的属性和自定义属性。 有关如何使用详细信息**DelProperty**指令，请参阅[INF AddProperty 指令和 INF DelProperty 指令](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)。

<a href="" id="featurescore-featurescore"></a>**FeatureScore=**<em>featurescore</em>  
**警告**   **FeatureScore**中直接指定时，只处理指令**\[DDInstall\]** 部分。

 

(Windows Vista 及更高版本)此指令的驱动程序，基于一个驱动程序支持的功能提供其他排名条件。 例如，可能会为定义特征评分[设备安装程序类](device-setup-classes.md)的区分特定于类的条件的驱动程序。

有关如何进行排名的驱动程序的详细信息，请参阅[如何 Windows Ranks Drivers （Windows Vista 和更高版本）](how-setup-ranks-drivers--windows-vista-and-later-.md)。

有关此指令的详细信息，请参阅[ **INF FeatureScore 指令**](inf-featurescore-directive.md)。

**请注意**  虽然*DDInstall*部分可以包含多个**FeatureScore**条目，只有第一项都处理的部分。

 

<a href="" id="bitreg-bit-registry-section--bit-registry-section----"></a>**BitReg=**<em>bit-registry-section</em>\[**,**<em>bit-registry-section</em>\]...  
此指令引用一个或多个 INF 编写器定义哪些现有注册表值条目中的部分类型[REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)进行修改。

**HKR**规范位注册表节中的指定 **...类\\**<em>SetupClassGUID</em>**\\**<em>设备实例 id</em>用户可访问驱动程序的注册表路径。 这种类型的**HKR**规范也称为。 "软件密钥"。

有关详细信息，请参阅[ **INF BitReg 指令**](inf-bitreg-directive.md)。

<a href="" id="logconfig-log-config-section--log-config-section----"></a>**LogConfig=**<em>log-config-section</em>\[**,**<em>log-config-section</em>\]...  
此指令引用一个或多个 INF 编写器定义中对于根枚举设备或手动安装的设备 INF 部分。 在这些命名部分，为此类的"检测到"或手动安装设备 INF 指定设备必须具有可操作的总线相对硬件资源的一个或多个逻辑的配置。 此外应具有此类的不是软件可配置的手动安装设备 INF <em>DDInstall</em>**。FactDef**部分。

**LogConfig**指令永远不会用于安装插即用 (PnP) 设备。 但是，可以使用[ **INF DDInstall.LogConfigOverride 部分**](inf-ddinstall-logconfigoverride-section.md)提供即插即用设备的重写配置。

此指令是相关的所有更高级别的 （未经） 驱动程序和组件。

有关详细信息，请参阅[ **INF LogConfig 指令**](inf-logconfig-directive.md)。

<a href="" id="profileitems-profile-items-section--profile-items-section----"></a>**ProfileItems=**<em>profile-items-section</em>\[**,**<em>profile-items-section</em>\]...  
（Microsoft Windows 2000 和更高版本的 Windows）此指令引用一个或多个 INF 编写器定义各节描述要添加或从开始菜单中删除的项。

有关详细信息，请参阅[ **INF ProfileItems 指令**](inf-profileitems-directive.md)。

<a href="" id="updateinis-update-ini-section--update-ini-section----"></a>**UpdateInis =**<em>更新 ini 部分</em>\[**，**<em>更新 ini 部分</em>\]...  
此很少使用的指令引用了一个或多个 INF 编写器定义的部分，指定源 INI 文件的特定部分或此类部分中的行是在安装过程中要读取到目标 INI 文件中具有相同名称。 （可选） 可以在更新 ini 部分中指定行的行的修改在目标上现有的 INI 文件从给定的源 INI 文件具有相同名称。

有关详细信息，请参阅[ **INF UpdateInis 指令**](inf-updateinis-directive.md)。

<a href="" id="updateinifields-update-inifields-section--update-inifields-section----"></a>**UpdateIniFields =**<em>更新 inifields 部分</em>\[**，**<em>更新 inifields 部分</em>\]...  
此很少使用的指令引用一个或多个 INF 编写器定义的部分指定特定于设备的 INI 文件的行内的修改。

有关详细信息，请参阅[ **INF UpdateIniFields 指令**](inf-updateinifields-directive.md)。

<a href="" id="ini2reg-ini-to-registry-section--ini-to-registry-section----"></a>**Ini2Reg =**<em>注册表部分 ini</em>\[**，**<em>注册表部分 ini</em>\]...  
这很少使用指令引用一个或多个 INF 编写器定义中的部分或在源媒体上，提供特定于设备的 INI 文件中的行部分是要移动到注册表。

有关详细信息，请参阅[ **INF Ini2Reg 指令**](inf-ini2reg-directive.md)。

<a href="" id="registerdlls-register-dll-section--register-dll-section----"></a>**RegisterDlls =**<em>注册 dll 部分</em>\[**，**<em>注册 dll 部分</em>\]...  
此指令引用用来指定 OLE 控件并需要自行注册的文件的一个或多个 INF 部分。

有关详细信息，请参阅[ **INF RegisterDlls 指令**](inf-registerdlls-directive.md)。

<a href="" id="unregisterdlls-unregister-dll-section--unregister-dll-section----"></a>**UnregisterDlls =**<em>注销 dll 部分</em>\[**，**<em>注销 dll 部分</em>\]...  
此指令引用用来指定 OLE 控件并需要自行注销 （自我删除） 的文件的一个或多个 INF 部分。

有关详细信息，请参阅[ **INF UnregisterDlls 指令**](inf-unregisterdlls-directive.md)。

<a href="" id="excludeid-device-identification-string--device-identification-string----"></a>**ExcludeID =**<em>设备标识字符串</em>\[**，**<em>设备标识字符串</em>\]...  
**警告**   **ExcludeID**中直接指定时，只处理指令**\[DDInstall\]** 部分。

 

(Windows XP 及更高版本)此指令指定了一个或多个设备标识字符串 (任一[硬件 Id](hardware-ids.md)或[兼容 Id](compatible-ids.md))。 *DDInstall*部分不会安装了设备[设备 Id](device-ids.md)与相匹配的硬件 Id 或兼容 Id 列出。

<a href="" id="reboot"></a>**Reboot**  
此指令指示调用方应提示完成安装后重新启动系统。

有关详细信息，请参阅[ **INF 重新启动指令**](inf-reboot-directive.md)。

<a name="remarks"></a>备注
-------

在 Windows Driver Kit (WDK) 文档中，术语*DDInstall*用来指*安装部分名称*用或者不用平台扩展。 因此，"*DDInstall*一节"意味着"INF，具有格式中的一个命名的部分\[*安装部分名称*\]或\[ <em>安装的部分名称</em>**.nt * * * xxx*\]"。 当您创建的名称*DDInstall*部分中，应包含特定于设备的前缀，如**\[WDMPNPB003_Device\]** 或者 **\[GPR400。Install.NT\]**。

每个*DDInstall*部分必须在每个制造商下的特定于设备/模型的项中引用[ **INF*模型*部分**](inf-models-section.md)的 INF 文件。

要传输的源媒体中没有关联文件的设备，除外，在不同的操作系统平台安装了 WDM 驱动程序的 INF 文件必须具有至少一个以下*DDInstall*部分：

- <em>安装的部分名称</em>**.ntx86** ，指定设备/驱动程序安装到基于 x86 的平台特定的条目的部分。
- <em>安装的部分名称</em>**.ntia64** ，指定对于特定于基于 Itanium 的平台的设备/驱动程序安装的条目的部分。
- <em>安装的部分名称</em>**.ntamd64** ，指定设备/驱动程序安装到基于 x64 的平台特定的条目的部分。
- <em>安装的部分名称</em>**.ntarm** ，指定设备/驱动程序安装到基于 ARM 的平台特定的条目的部分。
- <em>安装的部分名称</em>**.ntarm64** ，指定设备/驱动程序安装到基于 ARM64 的平台特定的条目的部分。


- *安装的部分名称*或<em>安装部分名称</em>**.nt**节指定并不特定于特定的设备/驱动程序安装的项硬件平台。

有关如何使用系统定义的详细信息 **.nt**， **.ntx86**， **.ntia64**， **.ntamd64**， **.ntarm**，并 **.ntarm64**扩展，请参阅[创建多个平台和操作系统的 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

从 Windows 2000 开始，安装驱动程序的 INF 文件必须具有[ **DDInstall.Services** ](inf-ddinstall-services-section.md)各节以指定要在注册表中存储的设备/驱动程序注册表信息 **...\\CurrentControlSet\\Services**树。 具体取决于该设备，它还可以具有一个或多个<em>DDInstall</em>**。HW**， <em>DDInstall</em>**。共同安装程序**， <em>DDInstall</em>**。接口**，和/或<em>DDInstall</em>**。LogConfigOverride**部分。

中的每个指令*DDInstall*部分可以引用多个部分名称。 但是，必须用逗号 （，） 分隔每个其他的指定的部分。

每个部分名称的 INF 文件中必须是唯一和必须遵从常规规则，用于定义的节名称。 有关这些规则的详细信息，请参阅[INF 文件的常规语法规则](general-syntax-rules-for-inf-files.md)。

任何**AddReg**中指定的指令*DDInstall*部分假定引用不能用于存储有关大写或较低的筛选器驱动程序的信息添加注册表部分多功能设备或有关驱动程序无关，但特定于设备的参数。 如果设备/驱动程序 INF 必须将此类信息存储在注册表中，它必须使用**AddReg**指令在其未修饰和修饰<em>DDInstall</em>**。HW**部分，如果有，以引用另一个 INF 编写器定义*添加注册表部分*。

具体取决于[设备安装程序类](device-setup-classes.md)中指定[ **INF 版本部分**](inf-version-section.md)，可以在中指定其他特定于类的指令*DDInstall*部分。 有关特定于类的指令的详细信息，请参阅以下主题：

-   [构建 Windows 边栏显示兼容设备 INF 文件](https://msdn.microsoft.com/library/windows/hardware/ff547750)
-   [DDInstall 网络 INF 文件中的部分](https://msdn.microsoft.com/library/windows/hardware/ff546332)
-   [静止图像设备 INF 文件](https://msdn.microsoft.com/library/windows/hardware/ff542762)
-   [WIA 设备 INF 文件](https://msdn.microsoft.com/library/windows/hardware/ff542770)
-   [网络组件的安装要求](https://msdn.microsoft.com/library/windows/hardware/ff554949)
-   [INF 文件中指定 WDF 指令](https://msdn.microsoft.com/windows/hardware/drivers/wdf/specifying-wdf-directives-in-inf-files)

<a name="examples"></a>示例
--------

此示例中显示的扩展*DDInstall*部分中， **Ser_Inst**并**Inp_Inst**。 这些部分中的示例引用[ **INF*模型*部分**](inf-models-section.md)。

```ini
[Ser_Inst]
CopyFiles=Ser_CopyFiles, mouclass_CopyFiles

[Ser_CopyFiles]
sermouse.sys

[mouclass_CopyFiles] ; section name referenced by > 1 CopyFiles
mouclass.sys

[Inp_Inst]
CopyFiles=Inp_CopyFiles, mouclass_CopyFiles

[Inp_CopyFiles]
inport.sys
```

下面的示例提供的常规说明，使用平台扩展：

```ini
[Manufacturer]
%MSFT% = Microsoft

[Microsoft]
%Device.DeviceDesc% = DeviceInstall, HWID
[DeviceInstall.NTx86]
;
; This section is used for installations on x86 systems.
;
...
[DeviceInstall.NTx86.Services]
;
; Services installation for x86 systems.
;
...
[DeviceInstall.NT]
;
; This section is used for installations on systems (all other architectures).
;
...
[DeviceInstall.NT.Services]
;
; Services installation for systems (all other architectures).
;
...
```

下面的示例演示*DDInstall*一部分安装在各种操作系统平台的音频设备的系统提供 WDM 驱动程序的 INF 文件：

```ini
[WDMPNPB003_Device.NT]
DriverVer=01/14/1999,5.0
Include=ks.inf, wdmaudio.inf
Needs=KS.Registration, WDMAUDIO.Registration.NT
LogConfig=SB16.LC1,SB16.LC2,SB16.LC3,SB16.LC4,SB16.LC5 
; a few log-config-sections omitted here for brevity
CopyFiles=MSSB16.CopyList
AddReg=WDM_SB16.AddReg
```

下面的示例显示由前面引用的各个部分**需要**中的系统提供的条目*ks.inf*并*wdmaudio.inf*文件。 在前面的示例中，这些文件中指定**包括**条目。 当操作系统的设备安装程序和/或媒体类安装程序处理此设备<em>安装部分名称</em>**.nt**部分中，还将处理这些接下来的两部分。

```ini
[KS.Registration]
; following AddReg= is actually a single line in the ks.inf file
AddReg=ProxyRegistration,CategoryRegistration,\
    TopologyNodeRegistration,PlugInRegistration,PinNameRegistration,\
    DeviceRegistration 
CopyFiles=KSProxy.Files,KSDriver.Files

[WDMAUDIO.Registration.NT]
AddReg=WDM.AddReg
CopyFiles=WDM.CopyFiles.Sys, WDM.CopyFiles.Drv
;
; INF-writer-defined add-registry and file-list sections
; referenced by preceding directives are omitted here for brevity
;
```

## <a name="see-also"></a>请参阅


[**AddProperty**](inf-addproperty-directive.md)

[***DDInstall*.CoInstallers**](inf-ddinstall-coinstallers-section.md)

[***DDInstall*.FactDef**](inf-ddinstall-factdef-section.md)

[***DDInstall *。硬件**](inf-ddinstall-hw-section.md)

[***DDInstall *。接口**](inf-ddinstall-interfaces-section.md)

[***DDInstall*.LogConfigOverride**](inf-ddinstall-logconfigoverride-section.md)

[***DDInstall*.Services**](inf-ddinstall-services-section.md)

[**DefaultInstall**](inf-defaultinstall-section.md)

[**DefaultInstall.Services**](inf-defaultinstall-services-section.md)

[**DelProperty**](inf-delproperty-directive.md)

[**FeatureScore**](inf-featurescore-directive.md)

 

 






