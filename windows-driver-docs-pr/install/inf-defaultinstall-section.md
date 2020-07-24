---
title: INF DefaultInstall 节
description: 如果在右键单击 INF 文件名后，用户选择 "安装" 菜单项，则会访问 INF 文件的 DefaultInstall 部分。
ms.assetid: 41412124-38d9-43c0-9954-d34b242a3922
keywords:
- INF DefaultInstall 部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF DefaultInstall Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b3dfbc7daa57d19e49e3fbc8aadcd9c579379ad
ms.sourcegitcommit: 5e5f3491e29f99b11a12b45da870043e0e92ddc5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86949033"
---
# <a name="inf-defaultinstall-section"></a>INF DefaultInstall 节


**注意**   如果你正在构建通用或移动驱动程序包，则此部分仅适用于体系结构装饰（例如） `[DefaultInstall.NTAMD64]` 。  或者，使用[**INF 制造商部分**](inf-manufacturer-section.md)。  在 INF 中同时使用**DefaultInstall**和**制造商**部分将导致通用 INF 验证失败，并可能导致不一致的安装行为。  请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

如果在右键单击 INF 文件名后，用户选择 "安装" 菜单项，则会访问 INF 文件的**DefaultInstall**部分。

```inf
[DefaultInstall] | 
[DefaultInstall.nt] | 
[DefaultInstall.ntx86] | 
[DefaultInstall.ntarm] | (Windows 8 and later versions of Windows)
[DefaultInstall.ntarm64]  (Windows 10 version 1709 and later versions of Windows)
[DefaultInstall.ntia64] | (Windows XP and later versions of Windows)
[DefaultInstall.ntamd64]  (Windows XP and later versions of Windows)
 
[CopyFiles=@filename | file-list-section[,file-list-section] ...]
[CopyINF=filename1.inf[,filename2.inf]...]
[AddReg=add-registry-section[,add-registry-section]...]
[Include=filename1.inf[,filename2.inf]...]
[Needs=inf-section-name[,inf-section-name]...]
[Delfiles=file-list-section[,file-list-section]...]
[Renfiles=file-list-section[,file-list-section]...]
[DelReg=del-registry-section[,del-registry-section]...]
[BitReg=bit-registry-section[,bit-registry-section]...]
[ProfileItems=profile-items-section[,profile-items-section]...]
[UpdateInis=update-ini-section[,update-ini-section]...]
[UpdateIniFields=update-inifields-section[,update-inifields-section]...]
[Ini2Reg=ini-to-registry-section[,ini-to-registry-section]...]
[RegisterDlls=register-dll-section[,register-dll-section]...]
[UnregisterDlls=unregister-dll-section[,unregister-dll-section]...] ...
```

## <a name="entries"></a>条目


<a href="" id="copyfiles--filename---file-list-section--file-list-section-----"></a>**CopyFiles = @**<em>filename</em>  |  *file-list* \[ **-section**<em>file-list-section</em> \] .。。  
此可选指令指定一个要从源媒体复制到目标的命名文件，或引用一个或多个由 INF 编写器定义的部分，这些部分指定要从源媒体传输到目标的文件。

INF 的**DestinationDirs**部分中的**DefaultDestDir**条目指定要复制的任何单个文件的目标。 " **SourceDisksNames** " 和 " **SourceDisksFiles** " 部分或在此 INF 的 "**版本**" 部分的 " **LAYOUTFILE** " 条目中指定的其他 INF，提供驱动程序文件在分发介质上的位置。

有关详细信息，请参阅[**INF CopyFiles 指令**](inf-copyfiles-directive.md)。

<a href="" id="copyinf-filename1-inf--filename2-inf----"></a>**CopyINF =**<em>filename1</em>**.inf** \[ **，**<em>filename2</em>**.inf** \] .。。  
（Windows XP 及更高版本的 Windows。）此指令将导致指定的 INF 文件复制到目标系统。

有关详细信息，请参阅[**INF CopyINF 指令**](inf-copyinf-directive.md)。

<a href="" id="addreg-add-registry-section--add-registry-section----"></a>**AddReg =**<em>添加注册表-节</em> \[ **，**<em>外</em>接程序 \] .。。  
此指令引用一个或多个由 INF 编写器定义的部分，其中，可能有初始值条目的新子项已被指定写入注册表或修改现有键的值项。

有关详细信息，请参阅[**INF AddReg 指令**](inf-addreg-directive.md)。

<a href="" id="include-filename1-inf--filename2-inf----"></a>**Include =**<em>filename1</em>**.inf** \[ **，**<em>filename2</em>**.inf** \] .。。  
此可选条目指定一个或多个系统提供的其他 INF 文件，其中包含安装此设备和/或驱动程序所需的部分。 如果指定此项，则通常是**需要**输入。

例如，依赖于系统内核流支持的设备驱动程序的系统 INF 文件指定此项，如下所示：

```inf
Include= ks.inf[,[kscaptur.inf,][ksfilter.inf]]
```

有关其用法的**包含**项和限制的详细信息，请参阅[指定设备文件的源位置和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**需求 =**<em>inf-名称</em> \[ **，**<em>inf-节名称</em> \] .。。  
此可选条目指定系统提供的 INF 文件中的部分，必须在安装此设备期间进行处理。 通常，此类命名部分为*DDInstall* （或<em>DDInstall</em>）**。**<em>xxx</em>）部分中列出**的一个 INF**文件中。 但是，它可以是在此类*DDInstall*或<em>DDInstall</em>中引用的任何部分 **。**<em>xxx</em>部分。

例如，具有上述**Include**条目的设备驱动程序的 INF 文件指定此项，如下所示：

```inf
Needs= KS.Registration[,KSCAPTUR.Registration | 
                        KSCAPTUR.Registration.NT,MSPCLOCK.Installation]
```

不能嵌套**需求**条目。 （有关使用的**需求**条目和限制的详细信息，请参阅[指定设备文件的源位置和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a href="" id="delfiles-file-list-section--file-list-section----"></a>**Delfiles =**<em>文件列表部分</em> \[ **，**<em>文件列表-节</em> \] .。。  
此指令引用一个或多个由 INF 写入器定义的部分，其中列出了要删除的目标上的文件。

有关详细信息，请参阅[**INF DelFiles 指令**](inf-delfiles-directive.md)。

<a href="" id="renfiles-file-list-section--file-list-section----"></a>**Renfiles =**<em>文件列表部分</em> \[ **，**<em>文件列表-节</em> \] .。。  
此指令引用一个或多个 INF 写入器定义的部分，其中列出了要在目标计算机上复制与设备相关的源文件之前在目标上重命名的文件。

有关详细信息，请参阅[**INF RenFiles 指令**](inf-renfiles-directive.md)。

<a href="" id="delreg-del-registry-section--del-registry-section----"></a>**DelReg =**<em>del-registry</em>-section \[ **，**<em>del</em> \] .。。  
此指令引用一个或多个由 INF 写入器定义的部分，其中在安装设备的过程中，已指定要从注册表中删除的项和/或值条目。

通常，此指令用于处理升级，因为 INF 必须从以前安装的此设备中清除旧的注册表项。 此类 "删除注册表" 一节中的**HKR**规范指定了 **。类 \\ **<em>SetupClassGUID</em> **\\** 用户可访问的驱动程序的<em>设备实例 id</em>注册表路径。 这种类型的**HKR**规范也称为。 "软件密钥"。

有关详细信息，请参阅[**INF DelReg 指令**](inf-delreg-directive.md)。

<a href="" id="bitreg-bit-registry-section--bit-registry-section----"></a>**BitReg =**<em>位注册表-节</em> \[ **，**<em>位注册表-节</em> \] .。。  
此指令引用一个或多个由 INF 写入器定义的部分，其中[REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)的类型的现有注册表值项被修改。 有关详细信息，请参阅[**INF AddReg 指令**](inf-addreg-directive.md)。

此类注册表部分中的**HKR**规范指定了 **。类 \\ **<em>SetupClassGUID</em> **\\** 用户可访问的驱动程序的<em>设备实例 id</em>注册表路径。 这种类型的**HKR**规范也称为。 "软件密钥"。

有关详细信息，请参阅[**INF BitReg 指令**](inf-bitreg-directive.md)。

<a href="" id="profileitems-profile-items-section--profile-items-section----"></a>**ProfileItems =**<em>profile-items-section</em> \[ **，**<em>profile-items</em> \] .。。  
此指令引用一个或多个由 INF 编写器定义的部分，这些部分描述要添加到 "开始" 菜单或从 "开始" 菜单中删除的项。

有关详细信息，请参阅[**INF ProfileItems 指令**](inf-profileitems-directive.md)。

<a href="" id="updateinis-update-ini-section--update-ini-section----"></a>**UpdateInis =**"<em>更新-ini-节</em> \[ **，**<em>更新-ini</em> \] ..."  
此很少使用的指令将引用一个或多个由 INF 编写器定义的部分，这些部分指定一个源 INI 文件，在该文件中，将在安装过程中将此部分中的特定节或行读取到同名的目标 INI 文件中。 （可选）可以在更新-INI 部分中指定同一名称的指定源 INI 文件对目标上的现有 INI 文件进行逐行修改。

有关详细信息，请参阅[**INF UpdateInis 指令**](inf-updateinis-directive.md)。

<a href="" id="updateinifields-update-inifields-section--update-inifields-section----"></a>**UpdateIniFields =**<em>inifields-section</em> \[ **，**<em>inifields-节</em> \] .。。  
此很少使用的指令引用一个或多个由 INF 编写器定义的部分，其中指定了设备特定 INI 文件的行中的修改。

有关详细信息，请参阅[**INF UpdateIniFields 指令**](inf-updateinifields-directive.md)。

<a href="" id="ini2reg-ini-to-registry-section--ini-to-registry-section----"></a>**Ini2Reg =**<em>ini 到注册表-节</em> \[ **，**<em>ini 到注册表-节</em> \] .。。  
这种很少使用的指令引用一个或多个由 INF 编写器定义的部分，在这些部分中，源媒体上提供的特定于设备的 INI 文件中的部分或行会移动到注册表中。

有关详细信息，请参阅[**INF Ini2Reg 指令**](inf-ini2reg-directive.md)。

<a href="" id="registerdlls-register-dll-section--register-dll-section----"></a>**RegisterDlls =**<em>register-dll-节</em> \[ **，**<em>寄存器-dll-节</em> \] .。。  
此指令引用一个或多个 INF 部分，这些部分用于指定作为 OLE 控件并且需要自注册的文件。

有关详细信息，请参阅[**INF RegisterDlls 指令**](inf-registerdlls-directive.md)。

<a href="" id="unregisterdlls-unregister-dll-section--unregister-dll-section----"></a>**UnregisterDlls =**<em>注销</em>-dll 节 \[ **，**<em>注销-节</em> \] .。。  
此指令引用一个或多个 INF 部分，这些部分用于指定作为 OLE 控件的文件，并需要自行注销（自行删除）。

有关详细信息，请参阅[**INF UnregisterDlls 指令**](inf-unregisterdlls-directive.md)。

<a name="remarks"></a>备注
-------

**DefaultInstall**部分不能用于设备安装。 仅将**DefaultInstall**部分用于安装类筛选器驱动程序、类共同安装程序、文件系统筛选器和与设备节点无关的内核驱动程序服务（*devnode*）。

**注意**   如果驱动程序包要进行数字签名，则[驱动程序包](driver-packages.md)的 inf 文件不得包含 inf **DefaultInstall**部分。 有关对驱动程序包进行签名的详细信息，请参阅[驱动程序签名](driver-signing.md)。

 

提供**DefaultInstall**部分是可选的。 如果 INF 文件不包括**DefaultInstall**部分，请在右键单击文件名后选择 "安装"，将会显示错误消息。

**注意**   与[***DDInstall***](inf-ddinstall-section.md)节不同， **DefaultInstall**节不能包含[**DriverVer**](inf-driverver-directive.md)或[**LogConfig**](inf-logconfig-directive.md)指令。

 

若要从*设备安装应用程序*安装**DefaultInstall**部分，请使用以下对**InstallHinfSection**的调用：

```inf
InstallHinfSection(NULL,NULL,TEXT("DefaultInstall 132 path-to-inf\infname.inf"),0); 
```

有关**InstallHinfSection**的详细信息，请参阅 Microsoft Windows SDK 文档。

有关如何使用**系统定义的** **ntx86**、 **ntia64**、 **ntamd64**、 **ntarm**和**Ntarm64**扩展的详细信息，请参阅[为多个平台和操作系统创建 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

<a name="examples"></a>示例
--------

以下示例显示了一个典型的**DefaultInstall**部分：

```inf
[DefaultInstall]
CopyFiles=MyAppWinFiles, MyAppSysFiles, @SRSutil.exe
AddReg=MyAppRegEntries
```

在此示例中，如果用户在右键单击 INF 文件名后选择 "安装"，则会执行**DefaultInstall**部分。

## <a name="see-also"></a>另请参阅


[***DDInstall***](inf-ddinstall-section.md)

[**DriverVer**](inf-driverver-directive.md)

[**LogConfig**](inf-logconfig-directive.md)

 

 






