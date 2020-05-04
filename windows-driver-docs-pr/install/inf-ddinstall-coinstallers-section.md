---
title: INF DDInstall.CoInstallers 节
description: CoInstallers 节注册一个或多个特定于设备的共同安装程序来补充现有设备类安装程序的操作。
ms.assetid: 2deb16e1-632a-4169-b718-7e3501e64562
keywords:
- INF DDInstall. CoInstallers 部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF DDInstall.CoInstallers Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88b6e3b29fd2b2081b19ad8117cda330ddb50777
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223259"
---
# <a name="inf-ddinstallcoinstallers-section"></a>INF DDInstall.CoInstallers 节


**注意**  如果您要构建通用或移动驱动程序包，此部分无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

此可选部分注册在分发媒体上提供的一个或多个特定于设备的共同安装程序，以补充现有设备类安装程序的操作。

```inf
[install-section-name.CoInstallers] |
[install-section-name.nt.CoInstallers] | 
[install-section-name.ntx86.CoInstallers] | 
[install-section-name.ntarm.CoInstallers] | (Windows 8 and later versions of Windows)
[install-section-name.ntarm64.CoInstallers] | (Windows 10 version 1709 and later versions of Windows)
[install-section-name.ntia64.CoInstallers] |  (Windows XP and later versions of Windows)
[install-section-name.ntamd64.CoInstallers]  (Windows XP and later versions of Windows)
  
AddReg=add-registry-section[,add-registry-section]... 
CopyFiles=@filename | file-list-section[,file-list-section]...
[Include=filename.inf[,filename2.inf]...]
[Needs=inf-section-name[,inf-section-name]...]
[DelFiles=file-list-section[,file-list-section]...]
[RenFiles=file-list-section[,file-list-section]...]
[DelReg=del-registry-section[,del-registry-section]...] 
[BitReg=bit-registry-section[,bit-registry-section]...]
[UpdateInis=update-ini-section[,update-ini-section]...]
[UpdateIniFields=update-inifields-section[,update-inifields-section]...]
[Ini2Reg=ini-to-registry-section[,ini-to-registry-section]...]
... 
```

## <a name="entries"></a>条目


<a href="" id="addreg-add-registry-section--add-registry-section----"></a>**AddReg =**<em>添加注册表-节</em>\[**，**<em>外</em>\]接程序 .。。  
引用一个或多个 INF 写入器定义的*外接程序*，它存储有关提供的共同安装程序的注册表信息。

在此类 "外接程序" 部分中指定的**HKR**指定 **。类\\****\\**<em>SetupClassGUID</em>用户可访问的驱动程序的<em>设备实例 id</em>注册表路径，也称为。 "软件密钥"。 因此，对于特定于设备的共同安装程序，它会在此用户可访问的每设备/驱动程序 "software" 子项中写入（或修改） **CoInstallers32**值条目。

对于特定于类的共同安装程序，它通过修改相应的的内容来注册新的共同安装程序 **。CoDeviceInstallers\\**<em>SetupClassGUID</em>子项。 必须在引用的 "添加注册表" 部分中显式指定相应注册表*SetupClassGUID*子项的路径。

有关详细信息，请参阅[**INF AddReg 指令**](inf-addreg-directive.md)。

<a href="" id="copyfiles--filename---file-list-section--file-list-section----"></a>**CopyFiles = @**<em>filename</em> | *file-list*\[**-section ...**<em>file-list-section</em>\]  
通常通过引用 INF 文件中其他位置的一个或多个 INF 写入器定义的*文件列表部分*，将源共同安装程序文件传输到目标计算机上的目标。 此类文件列表部分指定要从源媒体复制到目标目录的共同安装程序文件。

但是，安装共同安装程序的系统 INF 文件决不会在<em>DDInstall</em>中使用此指令 **。CoInstallers**部分。

有关详细信息，请参阅[**INF CopyFiles 指令**](inf-copyfiles-directive.md)。

<a href="" id="include-filename-inf--filename2-inf----"></a>**Include =**<em>filename</em>**.inf**\[**，**<em>filename2</em>\]...**.inf**  
指定一个或多个系统提供的其他 INF 文件，其中包含安装此设备或[设备安装程序类](device-setup-classes.md)的共同安装程序所需的部分。 如果指定此项，则通常是**需要**输入。 （有关使用的**包含**项和限制的详细信息，请参阅[指定设备文件的源位置和目标位置](specifying-the-source-and-target-locations-for-device-files.md)）。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**需求 =**<em>inf-名称</em>\[**，**<em>inf-节名称</em>\].。。  
指定在安装此设备过程中必须处理的特定部分。 通常，此类命名部分是<em>DDInstall</em>**。**"**包含**项" 中列出的系统提供的 INF 文件中的 CoInstallers 部分。 但是，它可以是在此类<em>DDInstall</em>中引用的任何部分 **。** 随附 INF 的 CoInstallers 部分。

不能嵌套**需求**条目。 有关其用法的**需求**条目和限制的详细信息，请参阅[指定设备文件的源位置和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a href="" id="delfiles-file-list-section--file-list-section----"></a>**DelFiles =**<em>文件列表部分</em>\[**，**<em>文件列表-节</em>\].。。  
引用文件列表部分，指定要从目标中删除的文件。 此指令很少使用。

有关详细信息，请参阅[**INF DelFiles 指令**](inf-delfiles-directive.md)。

<a href="" id="renfiles-file-list-section--file-list-section----"></a>**RenFiles =**<em>文件列表部分</em>\[**，**<em>文件列表-节</em>\].。。  
引用文件列表部分，指定在将共同安装程序源文件复制到目标之前要对其进行重命名的目标上的文件。 此指令也很少使用。

有关详细信息，请参阅[**INF RenFiles 指令**](inf-renfiles-directive.md)。

<a href="" id="delreg-del-registry-section--del-registry-section----"></a>**DelReg =**<em>del-registry</em>\[-section **，**<em>del</em>\].。。  
引用一个或多个 INF-编写器-定义删除--*节*。 此部分指定有关应从注册表中删除的同一设备的以前安装的相关安装程序的过时注册表信息。 在此类 "删除注册表" 部分中指定的**HKR**指定了与**AddReg**条目所述相同的注册表子项。 <em>DDInstall</em>中非常少使用此指令 **。CoInstallers**部分。

有关详细信息，请参阅[**INF DelReg 指令**](inf-delreg-directive.md)。

<a href="" id="bitreg-bit-registry-section--bit-registry-section----"></a>**BitReg =**<em>位注册表-节</em>\[**，**<em>位注册表-节</em>\].。。  
此项在此部分有效，但几乎从未使用过。 此类注册表部分中指定的**HKR**指定了与**AddReg**条目所述相同的注册表子项。

有关详细信息，请参阅[**INF BitReg 指令**](inf-bitreg-directive.md)。

<a href="" id="updateinis-update-ini-section--update-ini-section----"></a>**UpdateInis = "**<em>更新-ini-节</em>\[**，**<em>更新-ini</em>\]..."  
此项在此部分有效，但几乎从未使用过。

有关详细信息，请参阅[**INF UpdateInis 指令**](inf-updateinis-directive.md)。

<a href="" id="updateinifields-update-inifields-section--update-inifields-section----"></a>**UpdateIniFields =**<em>inifields-section</em>\[**，**<em>inifields-节</em>\].。。  
此项在此部分有效，但几乎从未使用过。

有关详细信息，请参阅[**INF UpdateIniFields 指令**](inf-updateinifields-directive.md)。

<a href="" id="ini2reg-ini-to-registry-section--ini-to-registry-section----"></a>**Ini2Reg =**<em>ini 到注册表-节</em>\[**，**<em>ini 到注册表-节</em>\].。。  
此项在此部分有效，但几乎从未使用过。

有关详细信息，请参阅[**INF Ini2Reg 指令**](inf-ini2reg-directive.md)。

<a name="remarks"></a>备注
-------

在 INF 文件的 "每制造商"*型号*部分下，必须在特定于设备/模型的条目中引用指定的*DDInstall*部分。

INF 是否包含<em>DDInstall</em>**。Coinstallers**节中，每个平台修饰和未修饰*DDInstall*部分必须有一个。 例如，如果某一 inf 包含**\[**<em>安装节名称</em>**. ntx86\] **部分和一个**\[**<em>安装节名称</em>**\]** 部分，并且它注册了特定于设备的共同**\[**<em>安装程序，</em>则 inf 必须同时包含**ntx86。Coinstallers\] **部分和**\[**<em>安装节名称</em>**。Coinstallers\] **部分。 有关如何使用**系统定义的** **ntx86**、 **ntia64**、 **ntamd64**、 **ntarm**和**Ntarm64**扩展的详细信息，请参阅[为多个平台和操作系统创建 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

<em>DDInstall</em>中的每个指令 **。CoInstallers**节可以引用多个 INF 写入器定义的部分名称。 但是，必须使用逗号（，）将每个附加的命名节与下一节隔开。

每个指令创建的节名称在 INF 文件中必须唯一，并且必须遵循用于定义节名称的常规规则。 有关这些规则的详细信息，请参阅[INF 文件的一般语法规则](general-syntax-rules-for-inf-files.md)。

共同安装程序是一个 Win32 DLL，通常会将额外的配置信息写入注册表，或者执行需要动态生成的特定于系统的信息，在创建 INF 时该信息不可用。 设备特定的联合安装程序补充了操作系统设备安装程序的安装操作，或在安装该设备时相应的类安装程序的安装操作。

有关如何编写和使用共同安装程序的详细信息，请参阅[编写共同安装程序](writing-a-co-installer.md)。

### <a name="installing-co-installer-images"></a>安装共同安装程序映像

所有共同安装程序文件都必须复制到 *% SystemRoot%\\system32*目录中。 与任何 INF **CopyFiles**操作一样，目标是通过*dirid*值**11**为 inf 文件的[**DestinationDirs**](inf-destinationdirs-section.md)部分中的命名*文件列表部分*显式控制的，或者为**DefaultDestDir**条目提供此*dirid*值。

### <a name="registering-device-specific-co-installers"></a>注册特定于设备的共同安装程序

注册一个或多个特定于设备的共同安装程序需要将[REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)类型的值项添加到注册表中。 使用以下常规格式指定[**AddReg**](inf-addreg-directive.md)指令引用的*添加注册表部分*：

```inf
[DDInstall.CoInstallers_DeviceAddReg]
 
HKR,,CoInstallers32,0x00010000,"DevSpecificCoInstall.dll
   [,DevSpecificEntryPoint]"[,"DevSpecific2CoInstall.dll
      [,DevSpecific2EntryPoint]"...] 
```

**HKR**条目作为 INF 文件中的一行列出，提供的每个特定于设备的共同安装程序 DLL 都必须具有唯一的名称。 注册列出的共同安装程序后，系统的设备安装程序将在该设备的每次安装过程的后续步骤中调用它们。

如果省略了可选的*DevSpecificEntryPoint* ，则将使用默认的**CoDeviceInstall**例程名称作为共同安装程序 DLL 的入口点。

有关详细信息，请参阅[注册设备特定的共同安装程序](registering-a-device-specific-co-installer.md)。

### <a name="registering-device-class-co-installers"></a>注册设备类共同安装程序

若要将一个或多个设备-类共同安装程序的值项（如果尚不存在）添加到注册表中，请使用[**AddReg**](inf-addreg-directive.md)指令引用的*添加注册表部分*：

```inf
[DDInstall.CoInstallers_ClassAddReg]
 
HKLM,System\CurrentControlSet\Control
    \CoDeviceInstallers,{SetupClassGUID},
       0x00010008,"DevClssCoInst.dll[,DevClssEntryPoint]" 
 ...
```

此类 "外接程序" 部分中的每个条目都作为 INF 文件中的一行列出，并且每个提供的类共同安装程序 DLL 都必须具有唯一的名称。 如果应将提供的共同安装程序用于多个[设备安装程序类](device-setup-classes.md)，则此添加注册表部分可以包含多个条目，每个条目都有相应的*SetupClassGUID*值。

此类补充设备-类共同安装程序不得替换现有类安装程序的所有已注册的共同安装程序。 因此，类共同安装程序必须具有唯一的名称，并且必须将提供的[REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)类型值追加到 **{**<em>SetupClassGUID</em>**}** 子项中已存在的特定于类的共同安装程序条目（如*flags*值**0x0010008**中的**8**指示）。

**注意** 如果已注册同一名称的共同安装程序，则[setupapi.log](setupapi.md)函数绝不会将重复的<em>DevClssCoInstall</em>**追加到值**项。

 

可通过右键单击 "安装" 或通过调用**SetupInstallFromInfSection**激活附加设备类共同安装程序的 INF。

<a name="examples"></a>示例
--------

此示例显示了*DDInstall*。IrDA 串行网络适配器的**CoInstallers**部分。 系统提供的这些 IrDA （串行） Nic 的 INF 向系统 IrDA 类安装程序提供共同安装程序。

```inf
; DDInstall section
[PNP.NT]
AddReg=ISIR.reg, Generic.reg, Serial.reg
PromptForPort=0     ; This is handled by IRCLASS.DLL
LowerFilters=SERIAL ; This is handled by IRCLASS.DLL
BusType=14
Characteristics=0x4 ; NCF_PHYSICAL 

; ... PNP.NT.Services section omitted here
[PNP.NT.CoInstallers]
AddReg = ISIR.CoInstallers.reg 
; ...

[IRSIR.reg]
HKR, Ndi, HelpText, 0, %IRSIR.Help%
HKR, Ndi, Service, 0, "IRSIR"
HKR, Ndi\Interfaces, DefUpper, 0, "ndisirda"
HKR, Ndi\Interfaces, DefLower, 0, "nolower"
HKR, Ndi\Interfaces, UpperRange, 0, "ndisirda"
HKR, Ndi\Interfaces, LowerRange, 0, "nolower"

[Generic.reg]
HKR,,InfraredTransceiverType,0,"0"

[Serial.reg]
HKR,,SerialBased,0, "0"

[ISIR.CoInstallers.reg]
HKR,,CoInstallers32,0x00010000,"IRCLASS.dll,IrSIRClassCoInstaller"

; ... Services and Event Log registry sections omitted here
[Strings]
; ...
IRSIR.Help = "An IrDA serial infrared device is a built-in COM port or 
external transceiver which transmits infrared pulses. This NDIS 
miniport driver installs as a network adapter and binds to the FastIR 
protocol."
```

上述 PNP<strong>。NT.CoInstallers</strong>部分仅引用了特定于安装程序的*添加注册表*部分。 因为系统提供的 INF 安装了一组 IrDA 网络设备，所以它没有[**CopyFiles**](inf-copyfiles-directive.md)指令。 与所有系统 INF 文件一样，此 INF 文件使用其[**版本**](inf-version-section.md)部分中的**LayoutFile**条目将共同安装程序文件传输到目标。

请注意，任何<em>DDInstall</em>**。** IHV 或 OEM 提供的 INF 中的 CoInstallers 部分还包含**CopyFiles**指令以及[**SourceDisksNames**](inf-sourcedisksnames-section.md)和[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)部分。

## <a name="see-also"></a>另请参阅


[**AddReg**](inf-addreg-directive.md)

[**BitReg**](inf-bitreg-directive.md)

[**CopyFiles**](inf-copyfiles-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[**DelFiles**](inf-delfiles-directive.md)

[**DelReg**](inf-delreg-directive.md)

[**DestinationDirs**](inf-destinationdirs-section.md)

[**Ini2Reg**](inf-ini2reg-directive.md)

[**RenFiles**](inf-renfiles-directive.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**UpdateIniFields**](inf-updateinifields-directive.md)

**UpdateInis**
[**版本**](inf-version-section.md)

 

 






