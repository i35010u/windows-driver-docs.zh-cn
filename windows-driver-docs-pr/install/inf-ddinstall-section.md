---
title: INF DDInstall 节
description: 每个模型的每个 DDInstall 部分都包含一个可选的 DriverVer 指令，以及一个或多个用于引用 INF 文件中的其他命名部分的指令，此处显示的是最常指定的 INF 指令 CopyFiles 和 AddReg，列在此处。
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
ms.openlocfilehash: 4a3eba3b733cf8381efe9eb7768679c7f65069e0
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732843"
---
# <a name="inf-ddinstall-section"></a>INF DDInstall 节


每个模型的每个 *DDInstall* 部分都包含一个可选的 **DriverVer** 指令，以及一个或多个用于引用 INF 文件中的其他命名部分的指令，此处显示的是最常指定的 Inf 指令 **CopyFiles** 和 **AddReg**，列在此处。

这些指令引用的部分包含有关安装驱动程序文件并将特定于设备的信息和/或驱动程序特定的信息写入注册表的说明。

```inf
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

## <a name="entries"></a>项


<a href="" id="driverver-mm-dd-yyyy--x-y-v-z--"></a>**DriverVer =**<em>mm/dd/yyyy</em> \[ **，**<em>x.x.x.x</em>\]   
此可选条目指定 [驱动程序包](driver-packages.md)的版本信息。

有关如何指定此项的信息，请参阅 [**INF DriverVer 指令**](inf-driverver-directive.md)。

<a href="" id="copyfiles--filename---file-list-section--file-list-section-----"></a>**CopyFiles = @**<em>filename</em>  |  *file-list* \[ **-section**<em>file-list-section</em> \] .。。  
此指令指定要从源媒体复制到目标中的一个或多个由 INF 写入器定义的部分，这些区域中的源媒体上的设备相关文件用于传输到目标。 **CopyFiles**指令是可选的，但在大多数*DDInstall*部分中存在。

INF 的[**DestinationDirs**](inf-destinationdirs-section.md)部分中的**DefaultDestDir**条目指定要复制的任何单个文件的目标。 " [**SourceDisksNames**](inf-sourcedisksnames-section.md) " 和 " [**SourceDisksFiles**](inf-sourcedisksfiles-section.md) " 部分或在此 INF 的 "[**版本**](inf-version-section.md)" 部分的 " **LAYOUTFILE** " 条目中指定的其他 INF，提供驱动程序文件在分发介质上的位置。

有关详细信息，请参阅 [**INF CopyFiles 指令**](inf-copyfiles-directive.md)。

<a href="" id="copyinf-filename1-inf--filename2-inf----"></a>**CopyINF =**<em>filename1</em>**.inf** \[ **，**<em>filename2</em>**.inf** \] .。。  
 (Windows XP 及更高版本) 此指令将导致指定的 INF 文件复制到目标系统。

有关详细信息，请参阅 [**INF CopyINF 指令**](inf-copyinf-directive.md)。

<a href="" id="addreg-add-registry-section--add-registry-section----"></a>**AddReg =**<em>添加注册表-节</em> \[ **，**<em>外</em>接程序 \] .。。  
此指令引用一个或多个由 INF 编写器定义的部分，其中，可能有初始值条目的新子项已被指定写入注册表或修改现有键的值项。

此类 "外接程序" 部分中的**HKR**规范指定了 **。类 \\ **<em>SetupClassGUID</em> **\\** 用户可访问的驱动程序的<em>设备实例 id</em>注册表路径。 这种类型的 **HKR** 规范也称为。 "软件密钥"。

有关详细信息，请参阅 [**INF AddReg 指令**](inf-addreg-directive.md)。

<a href="" id="addproperty-add-registry-section--add-registry-section----"></a>**AddProperty =**<em>添加注册表-节</em> \[ **，**<em>外</em>接程序 \] .。。  
 (Windows Vista 及更高版本) 引用一个或多个 INF 文件部分，这些部分修改为设备实例设置的 [设备属性](device-properties.md) 。 只应使用 [**INF AddProperty 指令**](inf-addproperty-directive.md) 设置 windows Vista 或更高版本的 windows 操作系统的新设备实例属性。

对于之前在 Windows Server 2003、Windows XP 或 Windows 2000 上引入的设备实例属性以及具有相应注册表项值的设备实例属性，应继续使用 [**INF AddReg 指令**](inf-addreg-directive.md) 来设置设备实例属性。 这些准则适用于系统定义的属性和自定义属性。 有关如何使用 **AddProperty** 指令的详细信息，请参阅 [使用 inf ADDPROPERTY 指令和 inf DelProperty 指令](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)。

<a href="" id="include-filename1-inf--filename2-inf----"></a>**Include =**<em>filename1</em>**.inf** \[ **，**<em>filename2</em>**.inf** \] .。。  
此可选条目指定一个或多个系统提供的其他 INF 文件，其中包含安装此设备和/或驱动程序所需的部分。 如果指定此项，则通常是 **需要** 输入。

例如，依赖于系统内核流支持的设备驱动程序的系统 INF 文件指定此项，如下所示：

```inf
Include= ks.inf[, [kscaptur.inf,] [ksfilter.inf]]...
```

有关其用法的 **包含** 项和限制的详细信息，请参阅 [指定设备文件的源位置和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**需求 =**<em>inf-名称</em> \[ **，**<em>inf-节名称</em> \] .。。  
此可选条目指定系统提供的 INF 文件中的部分，必须在安装此设备期间进行处理。 通常，此类命名节是 *DDInstall* (或 <em>DDInstall</em>**。**<em>xxx</em>) **包含在包含** 项中的一个 INF 文件中的部分。 但是，它可以是在此类*DDInstall*或<em>DDInstall</em>中引用的任何部分 **。**<em>xxx</em>部分。

例如，具有上述 **Include** 条目的设备驱动程序的 INF 文件指定此项，如下所示：

```inf
Needs= KS.Registration[, KSCAPTUR.Registration | KSCAPTUR.Registration.NT, MSPCLOCK.Installation]
```

不能嵌套**需求**条目。 有关其用法的 **需求** 条目和限制的详细信息，请参阅 [指定设备文件的源位置和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a href="" id="delfiles-file-list-section--file-list-section----"></a>**Delfiles =**<em>文件列表部分</em> \[ **，**<em>文件列表-节</em> \] .。。  
此指令引用一个或多个由 INF 写入器定义的部分，其中列出了要删除的目标上的文件。

有关详细信息，请参阅 [**INF DelFiles 指令**](inf-delfiles-directive.md)。

<a href="" id="renfiles-file-list-section--file-list-section----"></a>**Renfiles =**<em>文件列表部分</em> \[ **，**<em>文件列表-节</em> \] .。。  
此指令引用一个或多个 INF 写入器定义的部分，其中列出了要在目标计算机上复制与设备相关的源文件之前在目标上重命名的文件。

有关详细信息，请参阅[**INF RenFiles 指令**](inf-renfiles-directive.md)。

<a href="" id="delreg-del-registry-section--del-registry-section----"></a>**DelReg =**<em>del-registry</em>-section \[ **，**<em>del</em> \] .。。  
此指令引用一个或多个由 INF 写入器定义的部分，其中在安装设备的过程中，已指定要从注册表中删除的项和/或值条目。

通常，此指令用于处理升级，因为 INF 必须从以前安装的此设备中清除旧的注册表项。

此类 "删除注册表" 一节中的**HKR**规范指定了 **。类 \\ **<em>SetupClassGUID</em> **\\** 用户可访问的驱动程序的<em>设备实例 id</em>注册表路径。 这种类型的 **HKR** 规范也称为。 "软件密钥"。

有关详细信息，请参阅 [**INF DelReg 指令**](inf-delreg-directive.md)。

<a href="" id="delproperty-add-registry-section--add-registry-section----"></a>**DelProperty =**<em>添加注册表-节</em> \[ **，**<em>外</em>接程序 \] .。。  
 (Windows Vista 及更高版本) 引用一个或多个 INF 文件部分，这些部分将删除为设备实例设置的 [设备属性](device-properties.md) 。 只应使用 [**INF DelProperty 指令**](inf-delproperty-directive.md) 删除 windows Vista 或更高版本的 windows 中新的设备实例属性。

对于之前在 Windows Server 2003、Windows XP 或 Windows 2000 上引入的设备实例属性以及具有相应注册表项值的设备实例属性，应继续使用 [**INF DelReg 指令**](inf-delreg-directive.md) 删除设备实例属性。 这些准则适用于系统定义的属性和自定义属性。 有关如何使用 **DelProperty** 指令的详细信息，请参阅 [使用 inf ADDPROPERTY 指令和 inf DelProperty 指令](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)。

<a href="" id="featurescore-featurescore"></a>**FeatureScore =**<em>FeatureScore</em>  
**警告**   仅当直接在** \[ \] DDInstall**节中指定时才处理**FeatureScore**指令。

 

 (Windows Vista 及更高版本) 此指令为基于驱动程序支持的功能的驱动程序提供附加排名标准。 例如，可能会为 [设备安装程序类](./overview-of-device-setup-classes.md) 定义功能分数，以便根据特定于类的条件来区分驱动程序。

有关如何对驱动程序进行排序的详细信息，请参阅 [windows (Windows Vista 和更高版本) 的驱动程序的方式 ](how-setup-ranks-drivers--windows-vista-and-later-.md)。

有关此指令的详细信息，请参阅 [**INF FeatureScore 指令**](inf-featurescore-directive.md)。

**注意**   尽管*DDInstall*节可以包含多个**FeatureScore**条目，但仅为该部分处理第一个条目。

 

<a href="" id="bitreg-bit-registry-section--bit-registry-section----"></a>**BitReg =**<em>位注册表-节</em> \[ **，**<em>位注册表-节</em> \] .。。  
此指令引用一个或多个由 INF 写入器定义的部分，其中 [REG_BINARY](/windows/desktop/SysInfo/registry-value-types) 的类型的现有注册表值项被修改。

此类注册表部分中的**HKR**规范指定了 **。类 \\ **<em>SetupClassGUID</em> **\\** 用户可访问的驱动程序的<em>设备实例 id</em>注册表路径。 这种类型的 **HKR** 规范也称为。 "软件密钥"。

有关详细信息，请参阅 [**INF BitReg 指令**](inf-bitreg-directive.md)。

<a href="" id="logconfig-log-config-section--log-config-section----"></a>**LogConfig =**<em>日志配置-节</em> \[ **，**<em>日志配置-节</em> \] .。。  
此指令引用一个或多个 inf 写入器为根枚举设备或手动安装的设备在 INF 中定义的部分。 在这些命名部分中，此类 "检测的" 或手动安装的设备的 INF 指定了一个或多个与总线相关的硬件资源的逻辑配置，设备必须具有该资源才能正常运行。 不是软件可配置的手动安装的此类设备的 INF 也应为 <em>DDInstall</em>**。FactDef** 部分。

**LogConfig**指令从不用于安装即插即用 (PnP) 设备。 但是，可以使用 [**INF DDInstall. LogConfigOverride 部分**](inf-ddinstall-logconfigoverride-section.md) 为 PnP 设备提供替代配置。

此指令与所有更高级别的 (nondevice) 驱动程序和组件无关。

有关详细信息，请参阅 [**INF LogConfig 指令**](inf-logconfig-directive.md)。

<a href="" id="profileitems-profile-items-section--profile-items-section----"></a>**ProfileItems =**<em>profile-items-section</em> \[ **，**<em>profile-items</em> \] .。。  
 (Microsoft Windows 2000 及更高版本的 Windows) 此指令引用一个或多个由 INF 编写器定义的部分，这些部分描述要添加到 "开始" 菜单或从 "开始" 菜单中删除的项。

有关详细信息，请参阅 [**INF ProfileItems 指令**](inf-profileitems-directive.md)。

<a href="" id="updateinis-update-ini-section--update-ini-section----"></a>**UpdateInis =**"<em>更新-ini-节</em> \[ **，**<em>更新-ini</em> \] ..."  
此很少使用的指令将引用一个或多个由 INF 编写器定义的部分，这些部分指定一个源 INI 文件，在该文件中，将在安装过程中将此部分中的特定节或行读取到同名的目标 INI 文件中。 （可选）可以在更新-INI 部分中指定同一名称的给定源 INI 文件对目标上的现有 INI 文件进行逐行修改。

有关详细信息，请参阅 [**INF UpdateInis 指令**](inf-updateinis-directive.md)。

<a href="" id="updateinifields-update-inifields-section--update-inifields-section----"></a>**UpdateIniFields =**<em>inifields-section</em> \[ **，**<em>inifields-节</em> \] .。。  
此很少使用的指令引用一个或多个由 INF 编写器定义的部分，其中指定了设备特定 INI 文件的行中的修改。

有关详细信息，请参阅 [**INF UpdateIniFields 指令**](inf-updateinifields-directive.md)。

<a href="" id="ini2reg-ini-to-registry-section--ini-to-registry-section----"></a>**Ini2Reg =**<em>ini 到注册表-节</em> \[ **，**<em>ini 到注册表-节</em> \] .。。  
这种很少使用的指令引用一个或多个由 INF 编写器定义的部分，在这些部分中，源媒体上提供的特定于设备的 INI 文件中的部分或行会移动到注册表中。

有关详细信息，请参阅 [**INF Ini2Reg 指令**](inf-ini2reg-directive.md)。

<a href="" id="registerdlls-register-dll-section--register-dll-section----"></a>**RegisterDlls =**<em>register-dll-节</em> \[ **，**<em>寄存器-dll-节</em> \] .。。  
此指令引用一个或多个 INF 部分，这些部分用于指定作为 OLE 控件并且需要自注册的文件。

有关详细信息，请参阅 [**INF RegisterDlls 指令**](inf-registerdlls-directive.md)。

<a href="" id="unregisterdlls-unregister-dll-section--unregister-dll-section----"></a>**UnregisterDlls =**<em>注销</em>-dll 节 \[ **，**<em>注销-节</em> \] .。。  
此指令引用一个或多个 INF 部分，该部分用于指定作为 OLE 控件的文件，并需要自行注销 (自行删除) 。

有关详细信息，请参阅 [**INF UnregisterDlls 指令**](inf-unregisterdlls-directive.md)。

<a href="" id="excludeid-device-identification-string--device-identification-string----"></a>**ExcludeID =**<em>设备标识</em>-字符串 \[ **，**<em>设备标识符</em> \] .。。  
**警告**   仅当直接在** \[ \] DDInstall**节中指定时才处理**ExcludeID**指令。

 

 (Windows XP 及更高版本) 此指令指定 ([硬件 id](hardware-ids.md) 或 [兼容 id](compatible-ids.md)) 的一个或多个设备标识字符串。 *DDInstall*部分不会安装设备[id](device-ids.md)与列出的任何硬件 id 或兼容 id 相匹配的设备。

<a href="" id="reboot"></a>**要求**  
此指令表明在安装完成后应提示调用方重新启动系统。

有关详细信息，请参阅 [**INF Reboot 指令**](inf-reboot-directive.md)。

<a name="remarks"></a>备注
-------

在整个 Windows 驱动程序工具包 (WDK) 文档中，术语 " *DDInstall* " 用于指带有或不带平台扩展的 *安装部分名称*。 因此，"*DDInstall* " 部分指的是 INF 内的命名节，格式为 " \[ *安装节名称*" \] 或 " \[ <em>安装节名称</em>， * *nt * * * xxx* \] "。 为*DDInstall*节创建名称时，应包含特定于设备的前缀，例如** \[ WDMPNPB003_Device \] **或** \[ GPR400。安装 NT \] **。

每个 *DDInstall* 部分必须在 inf 文件的 "每制造商 [**INF *型号* " 部分**](inf-models-section.md) 下的特定于设备/模型的条目中引用。

除了没有关联文件要从源媒体传输的设备之外，在不同的操作系统平台上安装 WDM 驱动程序的 INF 文件必须至少具有以下 *DDInstall* 部分之一：

- **Ntx86**节，用于指定特定于基于 x86 的平台的设备/驱动程序安装的<em>条目。</em>
- **Ntia64**节，用于指定特定于基于 Itanium 的平台的设备/驱动程序安装的<em>条目。</em>
- **Ntamd64**节，用于指定特定于基于 x64 的平台的设备/驱动程序安装的<em>条目。</em>
- **Ntarm**节，用于指定特定于基于 ARM 平台的设备/驱动程序安装的<em>条目。</em>
- Ntarm64<em>节，</em>**.ntarm64**用于指定特定于基于 ARM64 的平台的设备/驱动程序安装的条目。


- 用于指定不特定于特定硬件平台的设备/驱动程序安装条目的*安装部分名称*或<em>安装节名称</em>**。**

有关如何使用 **系统定义的** **ntx86**、 **ntia64**、 **ntamd64**、 **ntarm**和 **Ntarm64** 扩展的详细信息，请参阅 [为多个平台和操作系统创建 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

从 Windows 2000 开始，安装驱动程序的 INF 文件必须具有 [**DDInstall**](inf-ddinstall-services-section.md) 部分，以指定要存储在注册表 **... \\CurrentControlSet \\ 服务** 树。 根据设备，它还可以有一个或多个 <em>DDInstall</em>**。HW**、 <em>DDInstall</em>**。CoInstallers**、 <em>DDInstall</em>**。接口**和/或 <em>DDInstall</em>**。LogConfigOverride** 部分。

*DDInstall*节中的每个指令都可以引用多个部分名称。 但是，必须将每个附加的命名节与下一个逗号 ( ) 。

每个节名称在 INF 文件中必须唯一，并且必须遵循用于定义节名称的常规规则。 有关这些规则的详细信息，请参阅 [INF 文件的一般语法规则](general-syntax-rules-for-inf-files.md)。

假定在*DDInstall*节中指定的任何**AddReg**指令引用一个 "添加注册表" 部分，该部分不能用于存储有关较高或较低筛选器驱动程序的信息、有关多功能设备，或与驱动程序无关但特定于设备的参数。 如果设备/驱动程序 INF 必须将此类信息存储在注册表中，则必须在其修饰和修饰的<em>DDInstall</em>中使用**AddReg**指令 **。HW**部分（如果有）引用另一个 INF 写入器定义的*外接程序-部分*。

根据[**INF 版本部分**](inf-version-section.md)中指定的[设备安装程序类](./overview-of-device-setup-classes.md)，可以在*DDInstall*节中指定其他特定于类的指令。 有关特定于类的指令的详细信息，请参阅以下主题：

-   [为 Windows 边栏显示兼容设备生成 INF 文件](../index.yml)
-   [网络 INF 文件中的 DDInstall 节](../network/ddinstall-services-section-in-a-network-inf-file.md)
-   [静态图像设备的 INF 文件](../image/inf-files-for-still-image-devices.md)
-   [WIA 设备的 INF 文件](../image/inf-files-for-wia-devices.md)
-   [网络组件的安装要求](../network/installation-requirements-for-network-adapters.md)
-   [在 INF 文件中指定 WDF 指令](../wdf/specifying-wdf-directives-in-inf-files.md)

<a name="examples"></a>示例
--------

此示例显示了 *DDInstall* 部分的扩展 **Ser_Inst** 和 **Inp_Inst**。 在 [**INF *模型* 部分**](inf-models-section.md)的示例中引用了这些部分。

```inf
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

以下示例提供了使用平台扩展的一般说明：

```inf
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

以下示例显示了一个 INF 文件的 *DDInstall* 部分，该文件在各种操作系统平台上为音频设备安装系统提供的 WDM 驱动程序：

```inf
[WDMPNPB003_Device.NT]
DriverVer=01/14/1999,5.0
Include=ks.inf, wdmaudio.inf
Needs=KS.Registration, WDMAUDIO.Registration.NT
LogConfig=SB16.LC1,SB16.LC2,SB16.LC3,SB16.LC4,SB16.LC5 
; a few log-config-sections omitted here for brevity
CopyFiles=MSSB16.CopyList
AddReg=WDM_SB16.AddReg
```

下面的示例显示了系统提供的*wdmaudio*文件中前面的**需求**条目引用的*部分。* 在前面的示例中，这些文件在 " **包括** " 项中指定。 当操作系统的设备安装程序和/或媒体类安装程序处理此设备的 <em>安装部分名称</em>**nt** 部分时，还会处理下面两个部分。

```inf
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

## <a name="see-also"></a>另请参阅


[**AddProperty**](inf-addproperty-directive.md)

[***DDInstall*.CoInstallers**](inf-ddinstall-coinstallers-section.md)

[***DDInstall*.FactDef**](inf-ddinstall-factdef-section.md)

[***DDInstall*.HW**](inf-ddinstall-hw-section.md)

[***DDInstall*.接口**](inf-ddinstall-interfaces-section.md)

[***DDInstall*.LogConfigOverride**](inf-ddinstall-logconfigoverride-section.md)

[***DDInstall*.服务器**](inf-ddinstall-services-section.md)

[**DefaultInstall**](inf-defaultinstall-section.md)

[**DefaultInstall**](inf-defaultinstall-services-section.md)

[**DelProperty**](inf-delproperty-directive.md)

[**FeatureScore**](inf-featurescore-directive.md)

