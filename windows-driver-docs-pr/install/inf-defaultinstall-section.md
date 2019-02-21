---
title: INF DefaultInstall 部分
description: 如果用户的 INF 文件的名称上右键单击后选择"安装"菜单项，访问的 INF 文件 DefaultInstall 部分。
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
ms.openlocfilehash: e88d0693ed72ea338b7a7287838bb9b7d168bb17
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542910"
---
# <a name="inf-defaultinstall-section"></a>INF DefaultInstall 部分


**请注意**  如果要构建一个通用或移动设备的驱动程序包，此部分无效，不应使用。  相反，仅使用[ **INF 制造商部分**](inf-manufacturer-section.md)。  同时使用这二者**DefaultInstall**并**制造商**中你 INF 部分将会导致通用 INF 验证失败，可能会导致不一致的安装行为。  请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

INF 文件的**DefaultInstall**如果用户选择"安装"菜单项的 INF 文件的名称上右键单击后访问该部分。

```ini
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


<a href="" id="copyfiles--filename---file-list-section--file-list-section-----"></a>**CopyFiles = @**<em>文件名</em> | *文件列表部分*\[**，**<em>文件列表节</em>\] ...  
此可选指令指定要从源介质复制到目标，一个命名的文件，或者引用一个或多个 INF 编写器定义的部分指定要传输到目标的源媒体中的文件。

**DefaultDestDir**中的条目**DestinationDirs** INF 部分指定任何单个文件要复制的目标。 **SourceDisksNames**并**SourceDisksFiles**部分中或其他 INF 中指定**LayoutFile**条目此 INF**版本**部分中，驱动程序文件在分发媒体提供的位置。

有关详细信息，请参阅[ **INF CopyFiles 指令**](inf-copyfiles-directive.md)。

<a href="" id="copyinf-filename1-inf--filename2-inf----"></a>**CopyINF=**<em>filename1</em>**.inf**\[**,**<em>filename2</em>**.inf**\]...  
（Windows XP 和更高版本的 Windows。）此指令会导致指定的 INF 文件复制到目标系统。

有关详细信息，请参阅[ **INF CopyINF 指令**](inf-copyinf-directive.md)。

<a href="" id="addreg-add-registry-section--add-registry-section----"></a>**AddReg=**<em>add-registry-section</em>\[**,**<em>add-registry-section</em>\]...  
此指令引用一个或多个 INF 编写器定义指定的部分中的新子项，也可能包含初始值的条目，是要写入到注册表或中的现有密钥值项进行修改。

有关详细信息，请参阅[ **INF AddReg 指令**](inf-addreg-directive.md)。

<a href="" id="include-filename1-inf--filename2-inf----"></a>**Include=**<em>filename1</em>**.inf**\[**,**<em>filename2</em>**.inf**\]...  
此可选项指定一个或多个其他系统提供 INF 文件包含安装此设备和/或驱动程序所需的部分。 如果指定此项时，通常那么**需要**条目。

例如，依赖于系统的内核流支持的设备驱动程序的系统 INF 文件指定了该条目，如下所示：

```ini
Include= ks.inf[,[kscaptur.inf,][ksfilter.inf]]
```

有关详细信息**Include**条目和限制其使用时，请参阅[设备文件中指定的源和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**需要 =**<em>inf 部分名称</em>\[**，**<em>inf 部分名称</em>\]...  
此可选项指定必须在此设备的安装过程中处理的系统提供 INF 文件内的部分。 通常情况下，此类指定的部分是*DDInstall* (或<em>DDInstall</em>**。**<em>xxx</em>) 部分中所示的 INF 文件之一**Include**条目。 但是，它可以是任何部分此类中被引用*DDInstall*或<em>DDInstall</em>**。**<em>xxx</em>包含 INF 部分。

例如，已在前面的设备驱动程序的 INF 文件**Include**条目指定了该条目，如下所示：

```ini
Needs= KS.Registration[,KSCAPTUR.Registration | 
                        KSCAPTUR.Registration.NT,MSPCLOCK.Installation]
```

**需要**条目不能嵌套。 (有关详细信息**需要**条目和限制其使用时，请参阅[设备文件中指定的源和目标位置](specifying-the-source-and-target-locations-for-device-files.md))。

<a href="" id="delfiles-file-list-section--file-list-section----"></a>**Delfiles =**<em>文件列表部分</em>\[**，**<em>文件列表部分</em>\]...  
此指令引用一个或多个 INF 编写器定义部分列出要删除在目标上的文件。

有关详细信息，请参阅[ **INF DelFiles 指令**](inf-delfiles-directive.md)。

<a href="" id="renfiles-file-list-section--file-list-section----"></a>**Renfiles =**<em>文件列表部分</em>\[**，**<em>文件列表部分</em>\]...  
此指令引用一个或多个 INF 编写器定义部分列出要重命名目标上之前设备相关的源代码文件复制到目标计算机的文件。

有关详细信息，请参阅[ **INF RenFiles 指令**](inf-renfiles-directive.md)。

<a href="" id="delreg-del-registry-section--del-registry-section----"></a>**DelReg=**<em>del-registry-section</em>\[**,**<em>del-registry-section</em>\]...  
此指令引用一个或多个 INF 编写器定义指定的部分中的密钥和/或值的条目是在设备的安装过程中从注册表中删除。

通常情况下，此指令用于处理升级时 INF 必须清理旧的注册表条目从以前安装的此设备。 **HKR**规范中删除注册表部分指定 **...类\\**<em>SetupClassGUID</em>**\\**<em>设备实例 id</em>用户可访问驱动程序的注册表路径。 这种类型的**HKR**规范也称为。 "软件密钥"。

有关详细信息，请参阅[ **INF DelReg 指令**](inf-delreg-directive.md)。

<a href="" id="bitreg-bit-registry-section--bit-registry-section----"></a>**BitReg=**<em>bit-registry-section</em>\[**,**<em>bit-registry-section</em>\]...  
此指令引用一个或多个 INF 编写器定义哪些现有注册表值条目中的部分类型[REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)进行修改。 有关详细信息，请参阅[ **INF AddReg 指令**](inf-addreg-directive.md)。

**HKR**规范位注册表节中的指定 **...类\\**<em>SetupClassGUID</em>**\\**<em>设备实例 id</em>用户可访问驱动程序的注册表路径。 这种类型的**HKR**规范也称为。 "软件密钥"。

有关详细信息，请参阅[ **INF BitReg 指令**](inf-bitreg-directive.md)。

<a href="" id="profileitems-profile-items-section--profile-items-section----"></a>**ProfileItems=**<em>profile-items-section</em>\[**,**<em>profile-items-section</em>\]...  
此指令引用一个或多个 INF 编写器定义各节描述要添加或从开始菜单中删除的项。

有关详细信息，请参阅[ **INF ProfileItems 指令**](inf-profileitems-directive.md)。

<a href="" id="updateinis-update-ini-section--update-ini-section----"></a>**UpdateInis =**<em>更新 ini 部分</em>\[**，**<em>更新 ini 部分</em>\]...  
此很少使用的指令引用了一个或多个 INF 编写器定义的部分，指定源 INI 文件的特定部分或此类部分中的行是在安装过程中要读取到目标 INI 文件中具有相同名称。 （可选） 可以在更新 ini 部分中指定行的行的修改在目标上现有的 INI 文件从指定的源 INI 文件具有相同名称。

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

<a name="remarks"></a>备注
-------

**DefaultInstall**部分必须不应用于设备安装。 使用**DefaultInstall**仅对类的安装的部分筛选器驱动程序、 类共同安装程序、 文件系统筛选器，和不是与设备节点相关联的内核驱动程序服务 (*devnode*).

**请注意**  INF 文件[驱动程序包](driver-packages.md)不能包含 INF **DefaultInstall**部分如果驱动程序包已进行数字签名。 有关对驱动程序包进行签名的详细信息，请参阅[驱动程序签名](driver-signing.md)。

 

提供**DefaultInstall**部分是可选的。 如果一个 INF 文件不包含**DefaultInstall**部分中，选择"安装"后右键单击文件名称将导致显示一条错误消息。

**请注意**  与不同[ ***DDInstall*** ](inf-ddinstall-section.md)部分中， **DefaultInstall**部分不能包含[ **DriverVer** ](inf-driverver-directive.md)或[ **LogConfig** ](inf-logconfig-directive.md)指令。

 

若要安装**DefaultInstall**从部分*设备安装应用程序*，使用以下调用**InstallHinfSection**:

```ini
InstallHinfSection(NULL,NULL,TEXT("DefaultInstall 132 path-to-inf\infname.inf"),0); 
```

有关详细信息**InstallHinfSection**，请参阅 Microsoft Windows SDK 文档。

有关如何使用系统定义的详细信息 **.nt**， **.ntx86**， **.ntia64**， **.ntamd64**， **.ntarm**，并 **.ntarm64**扩展，请参阅[创建多个平台和操作系统的 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

<a name="examples"></a>示例
--------

下面的示例演示一个典型**DefaultInstall**部分：

```ini
[DefaultInstall]
CopyFiles=MyAppWinFiles, MyAppSysFiles, @SRSutil.exe
AddReg=MyAppRegEntries
```

在此示例中， **DefaultInstall**部分右键单击的 INF 文件名称之后执行如果用户选择"安装"。

## <a name="see-also"></a>另请参阅


[***DDInstall***](inf-ddinstall-section.md)

[**DriverVer**](inf-driverver-directive.md)

[**LogConfig**](inf-logconfig-directive.md)

 

 






