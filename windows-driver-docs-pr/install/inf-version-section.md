---
title: INF Version 节
description: 按照约定，版本部分显示第一个在 INF 文件中。 每个 INF 文件必须具有本部分中。
ms.assetid: 53e30950-28a3-4ae3-a351-a917b02c84a5
keywords:
- INF 版本部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF Version Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca8002a496726dc802953871c560a8f6d6ea69f0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325811"
---
# <a name="inf-version-section"></a>INF Version 节


按照约定，**版本**部分显示第一个在 INF 文件。 每个 INF 文件必须具有本部分中。

```ini
[Version]
 
Signature="signature-name"
[Class=class-name]
[ClassGuid={nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn}]
[Provider=%INF-creator%]
[ExtensionId={xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}]
[LayoutFile=filename.inf [,filename.inf]... ]  (Windows 2000 and Windows XP)
[CatalogFile=filename.cat]
[CatalogFile.nt=unique-filename.cat]
[CatalogFile.ntx86=unique-filename.cat]
[CatalogFile.ntia64=unique-filename.cat]  (Windows XP and later versions of Windows)
[CatalogFile.ntamd64=unique-filename.cat]  (Windows XP and later versions of Windows)
[CatalogFile.ntarm=unique-filename.cat]  (Windows 8 and later versions of Windows)
[CatalogFile.ntarm64=unique-filename.cat]  (Windows XP and later versions of Windows)

DriverVer=mm/dd/yyyy,w.x.y.z
[PnpLockDown=0|1] (Windows Vista and later versions of Windows)
[DriverPackageDisplayName=%driver-package-description%]
[DriverPackageType=PackageType]
```

## <a name="entries"></a>条目


<a href="" id="signature--signature-name-"></a>**Signature="**<em>signature-name</em>**"**  
必须是 **$Windows NT$** 或 **$Chicago$**。 这表示此 INF 的有效的操作系统。 这些签名值的含义如下。

| 签名值  | 含义                       |
|------------------|-------------------------------|
| **$Windows NT$** | 所有 Windows 操作系统 |
| **$Chicago$**    | 所有 Windows 操作系统 |

 

封闭的美元符号字符 （$） 是必需的但这些字符串不区分大小写。 如果*签名名称*为 none 的这些字符串值，该文件描述不属有效 INF。

通常情况下，Windows 不区分在这些签名值。 必须指定其中之一，但并不重要哪一个。 您应指定适当的值，以便人读取 INF 文件可以确定所针对的操作系统。

某些类安装程序将必须指定的签名值的方式上的其他要求。 此类要求，如果它们存在，设备特定于类型的各节论述了此 Windows Driver Kit (WDK)。

INF 必须通过追加到系统定义的扩展提供特定于操作系统的安装信息及其*DDInstall*部分中，是否*签名名称*是<strong>$Windows NT$</strong>或 **$Chicago$**。 (请参阅[创建多个平台和操作系统的 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)有关这些扩展的讨论。)

<a href="" id="class-class-name"></a>**Class=**<em>class-name</em>  
对于任何标准的类型的设备，这将指定的名称[设备安装程序类](device-setup-classes.md)类型的情况下使用此 INF 文件安装的设备。 此名称通常是一个系统定义的类名称，如**Net**或**显示器**中列出了这些*Devguid.h*。 有关详细信息，请参阅[System-Supplied 设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff553419)。

如果指定了 INF**类，** 还应指定相应系统定义的 GUID 值及其**ClassGUID**条目。 指定的任何预定义的设备安装程序类的设备匹配的 GUID 值可以安装设备，其驱动程序速度更快，因为这有助于系统安装程序代码，以优化其 INF 搜索。

如果 INF 向系统添加新的安装程序类的设备，它应提供唯一的不区分大小写*类名*不同于任何系统提供的类中的值*Devguid.h*。 长度*类名*字符串必须是 32 个字符或更少。 INF 必须指定新生成的 GUID 值**ClassGUID**条目。 另请参阅[ **INF ClassInstall32 部分**](inf-classinstall32-section.md)。

此项是相关的安装既不在预定义的设备安装程序类的新设备驱动程序，也不新的设备安装程序类 INF。

**请注意**  此项是必需的安装通过插即用 (PnP) 管理器的设备驱动程序。

 

<a href="" id="classguid--nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn-"></a>**ClassGuid={**<em>nnnnnnnn</em>**-***nnnn***-***nnnn***-***nnnn***-**<em>nnnnnnnnnnnn</em>**}**  
指定[设备安装程序类](device-setup-classes.md)GUID。 GUID 值格式如下所示，其中每个*n*是十六进制数字。

此 GUID 值在注册表中指定设备安装程序类子项 **...\\类**树中在其下进行编写的此 INF 文件从安装的设备驱动程序的注册表信息。 如果有的话，此特定于类的 GUID 值还标识设备和特定于类的属性页提供程序的类型的设备类安装程序。

为新[设备安装程序类](device-setup-classes.md)，必须指定新生成 INF **ClassGUID**值。 有关如何创建 Guid 的详细信息，请参阅[驱动程序中使用 Guid](https://msdn.microsoft.com/library/windows/hardware/ff565392)。 另请参阅设备安装程序类。

**请注意**  此项是必需的安装通过即插即用管理器的设备驱动程序。

**扩展 Id**创作扩展 INF 时 = {xxxxxxxx xxxx-xxxx-xxxx-在左右加上} 指定扩展 ID GUID。 GUID 值格式如下所示，其中每个*x*是十六进制数字。

INF 时创建扩展 INF 的初始版本，必须指定新生成**ExtensionId**值。 但是，当更新现有扩展 INF， **ExtensionId**必须保持不变，以便扩展 INF 的多个相关的版本是版本控制的多个而不是被视为独立扩展 Inf可能同时安装在同一设备实例上。 有关如何创作扩展 Inf 的详细信息，请参阅[使用扩展 INF 文件](using-an-extension-inf-file.md)。

**请注意**此项才时创建扩展 INF，需要通过指定标识`Class = Extension`和`ClassGuid = {e2f84ce7-8efa-411c-aa69-97454ca4cb57}`。
 

<a href="" id="provider--inf-creator-"></a>**Provider=%**<em>INF-creator</em>**%**  
标识提供程序的 INF 文件。 通常情况下，此值指定为**%** <em>OrganizationName</em> **%** 稍后 INF 文件中扩展的令牌[**字符串**](inf-strings-section.md)部分。 以字符为单位的提供程序名称的最大长度是 LINE_LEN。

例如，通常随系统提供的 INF 文件指定*INF 创建者*作为<strong>%</strong>Msft<strong>%</strong>并定义<strong>%</strong> Msft<strong>%="</strong>Microsoft<strong>"</strong>中其[**字符串**](inf-strings-section.md)部分。

**请注意**  此项是必需的安装通过即插即用管理器的设备驱动程序。

 



<a href="" id="catalogfile-filename-cat"></a>**CatalogFile=**<em>filename</em>**.cat**  
指定一个目录 (。*cat*) 文件要包含在分发媒体的设备/驱动程序。

当[驱动程序包](driver-packages.md)提交给 Microsoft 进行数字签名 WHQL 提供[编录文件](catalog-files.md)驱动程序包后 WHQL 已测试并分配给包的数字签名。 有关测试和 IHV 或 OEM 驱动程序包的签名的详细信息，请参阅[WHQL 版本签名](whql-release-signature.md)。 目录文件中未列出[ **SourceDisksFiles** ](inf-sourcedisksfiles-section.md)部分或[ **CopyFiles** ](inf-copyfiles-directive.md) INF 的指令。 Windows 假定目录文件在与 INF 文件相同的位置。

系统提供的 INF 文件永远不会具有**CatalogFile =** 条目因为操作系统验证的签名为针对此类 INF 所有系统提供*xxx.cat*文件。

<a href="" id="catalogfile-nt-unique-filename-cat--"></a>**CatalogFile.nt=**<em>unique-filename</em>**.cat** |  

<a href="" id="catalogfile-ntx86-unique-filename-cat--"></a>**CatalogFile.ntx86=**<em>unique-filename</em>**.cat** |  

<a href="" id="catalogfile-ntia64-unique-filename-cat--"></a>**CatalogFile.ntia64=**<em>unique-filename</em>**.cat** |  

<a href="" id="catalogfile-ntamd64-unique-filename-cat"></a>**CatalogFile.ntamd64=**<em>unique-filename</em>**.cat**  

<a href="" id="catalogfile-ntarm-unique-filename-cat"></a>**CatalogFile.ntarm=**<em>unique-filename</em>**.cat**  

<a href="" id="catalogfile-ntarm64-unique-filename-cat"></a>**CatalogFile.ntarm64=**<em>unique-filename</em>**.cat**  


指定与另一个的 INF 编写器已确定的唯一文件名称。*cat*目录文件扩展名。 如果省略了这些可选条目，给定**CatalogFile =**<em>filename.cat</em>用于验证 WDM 设备/驱动程序安装。

如果任何修饰**CatalogFile。*xxx* =**  INF 中存在项**版本**部分以及未修饰**CatalogFile =** 假定未修饰的条目条目，识别*filename.cat*用于验证设备安装、 驱动程序安装，还是两者都不指定修饰的项时这些平台上。

对具有任何跨平台设备驱动程序 INF 文件**CatalogFile =** 并**CatalogFile。**<em>xxx</em> **=** 条目必须提供每个这样的.cat 文件的唯一 IHV/OEM-确定名称。

有关如何使用系统定义的详细信息 **.nt**， **.ntx86**， **.ntia64**， **.ntamd64**， **.ntarm**，并 **.ntarm64**扩展，请参阅[创建多个平台和操作系统的 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

**请注意**  可以跨所有支持的平台使用相同的.cat 文件，因为此项的使用不要求或建议。 但是，必须使用此项，如果你想要创建驱动程序包的特定于平台的.cat 文件。

 

<a href="" id="driverver-mm-dd-yyyy--w-x-y-z-"></a>**DriverVer=** **mm/dd/yyyy**,**w.x.y.z**  
此项指定此 INF 文件安装的驱动程序的版本信息。 从 Windows 2000 开始，此项是必需的。

有关如何指定此项的信息，请参阅[ **INF DriverVer 指令**](inf-driverver-directive.md)。


<a href="" id="pnplockdown-0-1"></a>**PnpLockDown=0**|**1**  
指定是否插即用 (PnP) 可防止应用程序直接修改的文件的[驱动程序包的](driver-packages.md)INF 文件指定。 如果**PnpLockDown**指令设置为 1，即插即用可防止应用程序直接修改复制的 INF 文件**CopyFiles**指令。 否则，如果 INF 文件中不包含指令或指令的值设置为零，具有管理员权限的应用程序可以直接修改这些文件。 以这种方式保护的驱动程序文件嘿 *第三方受保护的驱动程序文件*。

若要确保的即插即用驱动程序安装的完整性，应用程序不应直接修改的驱动程序包 INF 文件复制的驱动程序文件。 应用程序只应使用 Windows 提供的设备安装机制更新即插即用驱动程序。

从 Windows Vista 开始，应设置驱动程序包**PnpLockDown**为 1，以防止应用程序直接修改驱动程序文件。 但是，某些卸载驱动程序包的现有应用程序直接删除驱动程序文件。 若要保持与这些应用程序兼容性**PnpLockDown**应将此类的驱动程序包的指令设置为零。

**请注意**  虽然即插即用在 Windows Vista 和更高版本的 Windows 上不需要的 INF 文件包含**PnpLockDown**指令以安装的驱动程序 PnP 在以后的 Windows 版本可能要求 INF 文件的即插即用[驱动程序包](driver-packages.md)包括**PnpLockDown**指令。

 

<a href="" id="driverpackagedisplayname--driver-package-description-"></a><strong>DriverPackageDisplayName=%</strong>driver-package-description<strong>%</strong>  
已弃用。 以前使用的驱动程序安装框架 (DIFx)。 有关 DIFx 不推荐使用的信息，请参阅[DIFx 准则](difx-guidelines.md)。

<a href="" id="driverpackagetype-packagetype"></a>**DriverPackageType=** *PackageType*  
已弃用。 以前使用的驱动程序安装框架 (DIFx)。 有关 DIFx 不推荐使用的信息，请参阅[DIFx 准则](difx-guidelines.md)。

<a name="remarks"></a>备注
-------

当[驱动程序包](driver-packages.md)通过 Microsoft Windows 硬件质量实验室 (WHQL) 测试 WHQL 返回 *.cat*目录文件复制到 IHV 或 OEM。 每个 *.cat*文件包含驱动程序包的经数字加密的签名。 IHV 或 OEM 必须列出这些 *.cat* INF 中的文件**版本**部分，必须提供在分发媒体上，在与 INF 文件相同的位置中的文件。 *.Cat*必须解压缩文件。

**请注意**  如果 INF**版本**部分不包括至少一个**CatalogFile**或 **CatalogFile.nt***xxx*条目，该驱动程序是视为未签名，并列出中的日期[ **DriverVer** ](inf-driverver-directive.md)指令不会显示通过 Windows。

 

有关详细信息，请参阅[驱动程序签名](signing-drivers-for-public-release--windows-vista-and-later-.md)。

<a name="examples"></a>示例
--------

下面的示例演示**版本**典型的简单设备驱动程序 INF，跟所需的部分[ **SourceDisksNames** ](inf-sourcedisksnames-section.md)和[ **SourceDisksFiles** ](inf-sourcedisksfiles-section.md)隐含在此示例中指定的条目的部分**版本**部分：

```ini
[Version]
Signature="$Windows NT$"
Class=SCSIAdapter
ClassGUID={4D36E97B-E325-11CE-BFC1-08002BE10318}
Provider=%INF_Provider%
CatalogFile=aha154_ntx86.cat
DriverVer=01/29/2010

[SourceDisksNames]
;
; diskid = description[, [tagfile] [, <unused>, subdir]]
;
1 = %Floppy_Description%,,,\WinNT

[SourceDisksFiles.x86]
;
; filename_on_source = diskID[, [subdir][, size]]
;
aha154x.sys = 1,\x86

; ...

[Strings]
INF_Provider="Adaptec"
Floppy_Description = "Adaptec Drivers Disk"
; ...
```

## <a name="see-also"></a>请参阅


[***DDInstall***](inf-ddinstall-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**Strings**](inf-strings-section.md)

 

 






