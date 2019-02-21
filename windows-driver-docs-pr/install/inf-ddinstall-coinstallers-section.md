---
title: INF DDInstall.CoInstallers 部分
description: 共同安装程序部分注册一个或多个特定于设备的共同安装程序来补充现有的设备类安装程序的操作。
ms.assetid: 2deb16e1-632a-4169-b718-7e3501e64562
keywords:
- INF DDInstall.CoInstallers 部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF DDInstall.CoInstallers Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca20eaff3c1cd2635149ffd883b9a1bd9c510adb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547161"
---
# <a name="inf-ddinstallcoinstallers-section"></a>INF DDInstall.CoInstallers 部分


**请注意**  如果要构建一个通用或移动设备的驱动程序包，此部分无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

此可选部分注册一个或多个特定于设备的共同安装程序分发媒体上提供了用于补充现有的设备类安装程序的操作。

```ini
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


<a href="" id="addreg-add-registry-section--add-registry-section----"></a>**AddReg=**<em>add-registry-section</em>\[**,**<em>add-registry-section</em>\]...  
引用了一个或多 INF 编写器的定义*添加注册表部分*的存储提供共同安装程序的注册表信息。

**HKR**指定在此类添加注册表部分指定 **...类\\**<em>SetupClassGUID</em>**\\**<em>设备实例 id</em>注册表路径的用户可访问驱动程序，这也称为。 "软件密钥"。 因此，特定于设备的共同安装程序，它将写入 （或修改） **CoInstallers32**值此用户可访问的每个设备/驱动程序"软件"的子项中的项目。

对于特定于类共同安装程序，它注册新的共同安装程序通过修改相应的内容 **...CoDeviceInstallers\\**<em>SetupClassGUID</em>子项。 相应的注册表路径*SetupClassGUID*子项必须显式指定引用-添加注册表部分中。

有关详细信息，请参阅[ **INF AddReg 指令**](inf-addreg-directive.md)。

<a href="" id="copyfiles--filename---file-list-section--file-list-section----"></a>**CopyFiles = @**<em>文件名</em> | *文件列表部分*\[**，**<em>文件列表节</em>\]...  
源共同安装程序将文件传输到目标的目标计算机上，通常通过引用一个或多 INF 编写器的定义*文件列表部分*s INF 文件中的其他位置。 此类的文件列表部分指定要复制到目标系统上的目标目录的源媒体中的辅助安装程序文件。

但是，安装共同安装程序的系统 INF 文件永远不会使用在此指令<em>DDInstall</em>**。共同安装程序**部分。

有关详细信息，请参阅[ **INF CopyFiles 指令**](inf-copyfiles-directive.md)。

<a href="" id="include-filename-inf--filename2-inf----"></a>**Include=**<em>filename</em>**.inf**\[**,**<em>filename2</em>**.inf**\]...  
指定一个或多个其他系统提供 INF 文件包含安装此设备的共同安装程序所需的部分或[设备安装程序类](device-setup-classes.md)。 如果指定此项时，通常那么**需要**条目。 (有关详细信息**Include**条目和限制其使用时，请参阅[设备文件中指定的源和目标位置](specifying-the-source-and-target-locations-for-device-files.md))。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**需要 =**<em>inf 部分名称</em>\[**，**<em>inf 部分名称</em>\]...  
指定必须在此设备的安装过程中处理的特定部分。 通常情况下，此类指定的部分是<em>DDInstall</em>**。共同安装程序**中列出系统提供 INF 文件中的节**Include**条目。 但是，它可以是任何部分此类中被引用<em>DDInstall</em>**。共同安装程序**包含 INF 部分。

**需要**条目不能嵌套。 有关详细信息**需要**条目和限制其使用时，请参阅[设备文件中指定的源和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a href="" id="delfiles-file-list-section--file-list-section----"></a>**DelFiles =**<em>文件列表部分</em>\[**，**<em>文件列表部分</em>\]...  
引用指定要从目标中删除的文件的文件列表部分。 此指令很少使用。

有关详细信息，请参阅[ **INF DelFiles 指令**](inf-delfiles-directive.md)。

<a href="" id="renfiles-file-list-section--file-list-section----"></a>**RenFiles =**<em>文件列表部分</em>\[**，**<em>文件列表部分</em>\]...  
引用指定目标要重命名之前共同安装程序源文件复制到目标上的文件的文件列表部分。 也很少使用此指令。

有关详细信息，请参阅[ **INF RenFiles 指令**](inf-renfiles-directive.md)。

<a href="" id="delreg-del-registry-section--del-registry-section----"></a>**DelReg=**<em>del-registry-section</em>\[**,**<em>del-registry-section</em>\]...  
引用一个或多个 INF-编写器的定义*删除注册表部分*s。 此类部分指定以前安装的相同应从注册表中删除的设备的共同安装程序的旧注册信息。 **HKR**指定在此类删除注册表部分指定如前面所述的相同的注册表子项**AddReg**条目。 在很少使用此指令<em>DDInstall</em>**。共同安装程序**部分。

有关详细信息，请参阅[ **INF DelReg 指令**](inf-delreg-directive.md)。

<a href="" id="bitreg-bit-registry-section--bit-registry-section----"></a>**BitReg=**<em>bit-registry-section</em>\[**,**<em>bit-registry-section</em>\]...  
此项在本部分中有效，但几乎从未使用过。 **HKR**中此类指定位注册表部分如前面所述的中指定相同的注册表子项**AddReg**条目。

有关详细信息，请参阅[ **INF BitReg 指令**](inf-bitreg-directive.md)。

<a href="" id="updateinis-update-ini-section--update-ini-section----"></a>**UpdateInis =**<em>更新 ini 部分</em>\[**，**<em>更新 ini 部分</em>\]...  
此项在本部分中有效，但几乎从未使用过。

有关详细信息，请参阅[ **INF UpdateInis 指令**](inf-updateinis-directive.md)。

<a href="" id="updateinifields-update-inifields-section--update-inifields-section----"></a>**UpdateIniFields =**<em>更新 inifields 部分</em>\[**，**<em>更新 inifields 部分</em>\]...  
此项在本部分中有效，但几乎从未使用过。

有关详细信息，请参阅[ **INF UpdateIniFields 指令**](inf-updateinifields-directive.md)。

<a href="" id="ini2reg-ini-to-registry-section--ini-to-registry-section----"></a>**Ini2Reg =**<em>注册表部分 ini</em>\[**，**<em>注册表部分 ini</em>\]...  
此项在本部分中有效，但几乎从未使用过。

有关详细信息，请参阅[ **INF Ini2Reg 指令**](inf-ini2reg-directive.md)。

<a name="remarks"></a>备注
-------

指定*DDInstall*部分必须在每个制造商下的特定于设备/模型的项中引用*模型*INF 文件部分。

如果包括 INF <em>DDInstall</em>**。共同安装程序**部分中，必须有一个为每个平台修饰和未修饰名*DDInstall*部分。 例如，如果包含 INF **\[**<em>安装部分名称</em>**.ntx86\]** 部分和一个 **\[**<em>安装的部分名称</em>**\]** 部分和它注册特定于设备的共同安装程序，那么 INF 必须同时包含 **\[**<em>安装的部分名称</em>**.ntx86。共同安装程序\]** 部分和一个**\[**<em>安装部分名称</em>**。共同安装程序\]** 部分。 有关如何使用系统定义的详细信息 **.nt**， **.ntx86**， **.ntia64**， **.ntamd64**， **.ntarm**，并 **.ntarm64**扩展，请参阅[创建多个平台和操作系统的 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

中的每个指令<em>DDInstall</em>**。共同安装程序**部分可以引用多个 INF 编写器定义的节名称。 但是，必须用逗号 （，） 分隔每个其他的指定的部分。

每个指令创建的节名称必须是唯一的 INF 文件中的和必须遵从常规规则，用于定义的节名称。 有关这些规则的详细信息，请参阅[INF 文件的常规语法规则](general-syntax-rules-for-inf-files.md)。

辅助安装程序是一个 Win32 DLL，它通常将写入注册表的其他配置信息或执行其他安装任务的需要动态生成的特定于系统创建 INF 时不可用的信息。 特定于设备的共同安装程序安装该设备时补充安装操作的操作系统的设备安装程序或相应的类安装程序。

有关如何编写和使用共同安装程序的详细信息，请参阅[编写共同安装程序](writing-a-co-installer.md)。

### <a name="installing-co-installer-images"></a>安装辅助安装程序映像

必须将所有辅助安装程序文件复制到 *%systemroot%\\system32*目录。 像任何 INF **CopyFiles**操作，目标显式控制的已命名*文件列表部分*中[ **DestinationDirs** ](inf-destinationdirs-section.md) INF 文件的部分*dirid*值**11**或通过提供此*dirid*值**DefaultDestDir**条目。

### <a name="registering-device-specific-co-installers"></a>注册特定于设备的共同安装程序

注册一个或多个特定于设备的共同安装程序要求将添加[REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)-类型化值对注册表项。 指定*添加注册表部分*所引用的[ **AddReg** ](inf-addreg-directive.md)指令，通过使用以下常规形式：

```ini
[DDInstall.CoInstallers_DeviceAddReg]
 
HKR,,CoInstallers32,0x00010000,"DevSpecificCoInstall.dll
   [,DevSpecificEntryPoint]"[,"DevSpecific2CoInstall.dll
      [,DevSpecific2EntryPoint]"...] 
```

**HKR**条目列出为 INF 文件中单个行和每个提供特定于设备的共同安装程序 DLL 必须具有唯一的名称。 列出共同安装程序已注册后，系统的设备安装程序会调用它们在安装过程的每个后续步骤为该设备。

如果可选*DevSpecificEntryPoint*省略，则默认**CoDeviceInstall**例程名称用作辅助安装程序 DLL 的入口点。

有关详细信息，请参阅[注册特定于设备的共同安装程序](registering-a-device-specific-co-installer.md)。

### <a name="registering-device-class-co-installers"></a>注册设备类共同安装程序

若要添加值项 （和安装程序类的子项，如果它已不存在） 的一个或多个设备类共同安装程序对注册表*添加注册表部分*所引用的[ **AddReg**](inf-addreg-directive.md)指令具有如下常规形式：

```ini
[DDInstall.CoInstallers_ClassAddReg]
 
HKLM,System\CurrentControlSet\Control
    \CoDeviceInstallers,{SetupClassGUID},
       0x00010008,"DevClssCoInst.dll[,DevClssEntryPoint]" 
 ...
```

此类添加注册表部分中的每个条目列出为 INF 文件中单个行和每个提供的类共同安装程序 DLL 必须具有唯一的名称。 如果提供共同安装程序应使用多个[设备安装程序类](device-setup-classes.md)，添加注册表本节可以有多个条目，每个都有相应*SetupClassGUID*值。

此类的补充设备类共同安装程序必须替换现有类安装程序的任何已注册共同安装程序。 因此，类共同安装程序必须具有唯一的名称和[REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)-必须追加提供的类型值 (由**8**中*标志*值**0x0010008**) 到特定于类共同安装程序项，如果有中, 已经存在 **{**<em>SetupClassGUID</em>**}** 子项。

**请注意** [SetupAPI](setupapi.md)函数永远不会追加重复<em>DevClssCoInstall</em>**.dll**值项是否具有相同名称的一个共同安装程序已到注册。

 

通过右键单击安装或通过调用可激活补充设备类共同安装程序的 INF **SetupInstallFromInfSection**。

<a name="examples"></a>示例
--------

此示例演示*DDInstall*。**共同安装程序**IrDA 串行网络适配器的部分。 系统提供的这些 IrDA （串行） Nic INF 提供给系统 IrDA 类安装程序的共同安装程序。

```ini
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

前面的 PNP<strong>。NT。共同安装程序</strong>部分只能引用一个共同 installer 特定*添加注册表*部分。 它没有[ **CopyFiles** ](inf-copyfiles-directive.md)指令，因为此系统提供 INF 安装一组 IrDA 网络设备。 此 INF 文件使用所有系统 INF 文件，如**LayoutFile**中的条目及其[**版本**](inf-version-section.md)部分以共同安装程序文件传输到目标。

请注意的任何<em>DDInstall</em>**。共同安装程序**中由 IHV 或 OEM 提供 INF 部分还有**CopyFiles**指令，连同[ **SourceDisksNames** ](inf-sourcedisksnames-section.md)和[ **SourceDisksFiles** ](inf-sourcedisksfiles-section.md)部分。

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

 

 






