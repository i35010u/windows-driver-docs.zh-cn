---
title: INF Version 节
description: 按照约定，版本部分首先出现在 INF 文件中。 每个 INF 文件都必须包含此部分。
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
ms.openlocfilehash: 95dfc2bd2ce1cbb6e3f2df7abe0d0153a1d31131
ms.sourcegitcommit: 5ff30ddae453c6439177acde0e2d32eaf234a2c0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2020
ms.locfileid: "95030026"
---
# <a name="inf-version-section"></a>INF Version 节


按照约定， **版本** 部分首先出现在 INF 文件中。 每个 INF 文件都必须包含此部分。

```inf
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

## <a name="entries"></a>项


<a href="" id="signature--signature-name-"></a>**签名 = "**<em>签名-名称</em>**"**  
必须为 **NT $** 或 **$Chicago $**$Windows。 这表示此 INF 有效的操作系统。 这些签名值具有以下含义。

| 签名值  | 含义                       |
|------------------|-------------------------------|
| **$Windows NT $** | 所有 Windows 操作系统 |
| **$Chicago $**    | 所有 Windows 操作系统 |

 

 ($) 中需要包含美元符号字符，但这些字符串不区分大小写。 如果 *签名名称* 不是这些字符串值中的任何一个，则不接受文件作为有效 INF。

通常，Windows 不区分这些签名值。 必须指定其中的一个，但这并不重要。 你应指定适当的值，以便读取 INF 文件的其他人可以确定所需的操作系统。

某些类安装程序提出有关如何指定签名值的其他要求。 此类要求（如果存在）将在此 Windows 驱动程序工具包 (WDK) 的设备特定于设备的部分中进行讨论。

INF 必须通过将系统定义的扩展追加到其 *DDInstall* 部分来提供特定于操作系统的安装信息，无论 *签名名称* 是 <strong>$Windows NT $</strong>还是 **$Chicago $**。 有关这些扩展的讨论，请参阅 [为多个平台和操作系统创建 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md) (。 ) 

<a href="" id="class-class-name"></a>**类 =**<em>类名</em>  
对于任何标准类型的设备，此名称指定设备 [安装程序类](./overview-of-device-setup-classes.md) 的名称，该类型是使用该 INF 文件安装的设备的类型。 此名称通常是系统定义的类名称之一，例如 **Net** 或 **Display，** 它们列在 *Devguid* 中。 有关详细信息，请参阅 [系统提供的设备安装程序类](/windows-hardware/drivers/install/system-defined-device-setup-classes-reserved-for-system-use)。

如果 INF 指定了 **类，** 还应为其 **ClassGUID** 项指定相应的系统定义的 GUID 值。 为任何预定义的设备安装程序类的设备指定匹配 GUID 值可以更快地安装设备及其驱动程序，因为这有助于系统安装代码优化其 INF 搜索。

如果 INF 向系统中添加了一个新的设备安装类，则它应提供一个唯一的、不区分大小写的 *类名称* 值，该名称与 *Devguid* 中任何系统提供的类不同。 *类名称* 字符串的长度必须为32个字符或更少。 INF 必须为 **ClassGUID** 项指定新生成的 GUID 值。 另请参阅 [**INF ClassInstall32 部分**](inf-classinstall32-section.md)。

此条目与 INF 无关，后者在预定义的设备安装程序类和新的设备安装程序类下都不安装新的设备驱动程序。

**注意**  此项是通过即插即用 (PnP) manager 安装的设备驱动程序所必需的。

 

<a href="" id="classguid--nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn-"></a>**ClassGuid = {**<em>nnnnnnnn</em> **-** _nnnn_ *_-_* _nnnn_ *_-_* _nnnn_ *_-_* <em>nnnnnnnnnnnn</em>**}**  
指定 [设备安装程序类](./overview-of-device-setup-classes.md) GUID。 GUID 值的格式如下所示，其中每个 *n* 都是十六进制数字。

此 GUID 值指定注册表中的设备安装程序类子项 **... \\类** 树，用于写入从此 INF 文件中安装的设备驱动程序的注册表信息。 此类特定的 GUID 值还为设备类型和类特定属性页提供程序（如果有）标识设备类安装程序。

对于新的 [设备安装程序类](./overview-of-device-setup-classes.md)，INF 必须指定新生成的 **ClassGUID** 值。 有关如何创建 Guid 的详细信息，请参阅 [在驱动程序中使用 guid](../kernel/using-guids-in-drivers.md)。 另请参阅设备安装程序类。

**注意**  对于通过 PnP 管理器安装的设备驱动程序，此项是必需的。

**ExtensionId**= {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx} 在创作扩展 INF 时指定扩展 ID GUID。 GUID 值的格式如下所示，其中每个 *x* 是一个十六进制数字。

创建扩展 INF 的初始版本时，INF 必须指定新生成的 **ExtensionId** 值。 但是，在更新现有扩展 INF 时， **ExtensionId** 必须保持不变，以便将多个相关版本的扩展 inf 彼此版本控制，而不是被视为独立的扩展 inf，这两个版本可以同时安装在同一个设备实例上。 有关如何创作扩展 Inf 的详细信息，请参阅 [使用扩展 Inf 文件](using-an-extension-inf-file.md)。

**注意**  仅当创建扩展 INF 时才需要此项，这是通过指定 `Class = Extension` 和标识的 `ClassGuid = {e2f84ce7-8efa-411c-aa69-97454ca4cb57}` 。

**ClassVer =**<em>主要</em>**。**<em>次要</em>

除非设备类（如打印机）明确要求，否则系统将保留以供系统使用。 例如，请参阅 [V4 驱动程序 INF](../print/v4-driver-inf.md)。


<a href="" id="provider--inf-creator-"></a>**Provider =%**<em>INF-creator</em>**%**  
标识 INF 文件的提供程序。 通常，此项指定为 **%** <em>OrganizationName</em> **%** 标记，稍后会在 INF 文件的 [**字符串**](inf-strings-section.md)部分进行扩展。 提供程序名称的最大长度（以字符为 LINE_LEN）。

例如，随系统提供的 INF 文件通常将 *inf-creator* 指定为 <strong>%</strong> Msft <strong>%</strong> ，并 <strong>%</strong> 在其 [**字符串**](inf-strings-section.md)部分中定义 Msft <strong>% = "</strong>Microsoft <strong>"</strong> 。

**注意**  对于通过 PnP 管理器安装的设备驱动程序，此项是必需的。

 



<a href="" id="catalogfile-filename-cat"></a>**CatalogFile =**<em>filename</em>**.cat**  
指定目录 (。要包括在设备/驱动程序的分发介质上的 *cat*) 文件。

如果将 [驱动程序包](driver-packages.md) 提交给 Microsoft 进行数字签名，则在 whql 经过测试并为包分配数字签名后，whql 将为驱动程序包提供 [编录文件](catalog-files.md) 。 有关对 IHV 或 OEM 驱动程序包进行测试和签名的详细信息，请参阅 [WHQL 发行版签名](whql-release-signature.md)。 目录文件不会在 INF 的 [**SourceDisksFiles**](inf-sourcedisksfiles-section.md) 节或 [**CopyFiles**](inf-copyfiles-directive.md) 指令中列出。 Windows 假定目录文件与 INF 文件位于同一位置。

系统提供的 INF 文件从不具有 **CatalogFile =** 条目，因为操作系统会针对所有系统提供的 *xxx.cat* 文件验证此类 INF 的签名。

<a href="" id="catalogfile-nt-unique-filename-cat--"></a>**CatalogFile =**<em>唯一-filename</em>**.cat** |  

<a href="" id="catalogfile-ntx86-unique-filename-cat--"></a>**CatalogFile. ntx86 =**<em>唯一-filename</em>**.cat** |  

<a href="" id="catalogfile-ntia64-unique-filename-cat--"></a>**CatalogFile. ntia64 =**<em>唯一-filename</em>**.cat** |  

<a href="" id="catalogfile-ntamd64-unique-filename-cat"></a>**CatalogFile. ntamd64 =**<em>唯一-filename</em>**.cat**  

<a href="" id="catalogfile-ntarm-unique-filename-cat"></a>**CatalogFile. ntarm =**<em>唯一-filename</em>**.cat**  

<a href="" id="catalogfile-ntarm64-unique-filename-cat"></a>**CatalogFile. ntarm64 =**<em>唯一-filename</em>**.cat**  


指定另一个由 INF 编写器决定的唯一文件名，其中包含。目录文件的 *cat* 扩展。 如果省略这些可选项，则会使用给定的 **CatalogFile =**<em>FILENAME.CAT</em> 来验证 WDM 设备/驱动程序的安装。

如果任何修饰 **的 CatalogFile。*xxx* xxx =** 条目存在于 INF 的 **版本** 部分与未修饰的 **CatalogFile =** 条目中，假定未修饰的条目标识用于验证设备安装、驱动程序安装或未指定其修饰条目的那些平台上的 *filename.cat* 。

具有 **CatalogFile =** 和 CatalogFile 的任何跨平台设备驱动程序 INF 文件 **。**<em>xxx</em> **=** 条目必须为每个此类文件提供唯一的 IHV/OEM 确定的名称。

有关如何使用 **系统定义的** **ntx86**、 **ntia64**、 **ntamd64**、 **ntarm** 和 **Ntarm64** 扩展的详细信息，请参阅 [为多个平台和操作系统创建 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

**注意**  由于可以跨所有受支持的平台使用相同的 .cat 文件，因此不需要或建议使用此项。 但是，如果要为驱动程序包创建特定于平台的 .cat 文件，则必须使用此项。

 

<a href="" id="driverver-mm-dd-yyyy--w-x-y-z-"></a>**DriverVer =** **mm/dd/yyyy**，**w.x.y.z**  
此条目指定由此 INF 文件安装的驱动程序的版本信息。 从 Windows 2000 开始，此项是必需的。

有关如何指定此项的信息，请参阅 [**INF DriverVer 指令**](inf-driverver-directive.md)。


<a href="" id="pnplockdown-0-1"></a>**PnpLockDown = 0** |**1**  
指定即插即用 (PnP) 是否阻止应用程序直接修改 [驱动程序包的](driver-packages.md) INF 文件指定的文件。 如果 **PnpLockDown** 指令设置为1，则 PnP 会阻止应用程序直接修改由 INF **CopyFiles** 指令复制的文件。 否则，如果指令未包含在 INF 文件中，或者指令的值设置为零，则具有管理员权限的应用程序可以直接修改这些文件。 以这种方式进行保护的驱动程序文件称为 *第三方受保护的驱动程序文件*。

为了确保 PnP 驱动程序安装的完整性，应用程序不应直接修改驱动程序包 INF 文件所复制的驱动程序文件。 应用程序应仅使用 Windows 提供的用于更新 PnP 驱动程序的设备安装机制。

从 Windows Vista 开始，驱动程序包应将 **PnpLockDown** 设置为1，以防止应用程序直接修改驱动程序文件。 但是，某些卸载驱动程序包的现有应用程序会直接删除驱动程序文件。 为了保持与这些应用程序的兼容性，此类驱动程序包的 **PnpLockDown** 指令应该设置为零。

**注意**  尽管 Windows Vista 和更高版本的 Windows 上的 PnP 不需要 INF 文件包含 **PnpLockDown** 指令即可安装驱动程序，但在将来版本的 windows 中，pnp 可能要求 pnp [驱动程序包](driver-packages.md) 的 INF 文件包含 **PnpLockDown** 指令。

 

<a href="" id="driverpackagedisplayname--driver-package-description-"></a><strong>DriverPackageDisplayName =%</strong>驱动程序-包-说明<strong>%</strong>  
已弃用。 之前，驱动程序安装框架使用 (DIFx) 。 有关 DIFx 弃用的信息，请参阅 [DIFx 指导原则](difx-guidelines.md)。

<a href="" id="driverpackagetype-packagetype"></a>**DriverPackageType =** *PackageType*  
已弃用。 之前，驱动程序安装框架使用 (DIFx) 。 有关 DIFx 弃用的信息，请参阅 [DIFx 指导原则](difx-guidelines.md)。

<a name="remarks"></a>备注
-------

当 [驱动程序包](driver-packages.md) 通过 Microsoft Windows 硬件质量实验室 (WHQL) 测试时，whql 会将 *.cat* 目录文件返回到 IHV 或 OEM。 每个 *.cat* 文件都包含驱动程序包的数字加密签名。 IHV 或 OEM 必须列出 INF **版本** 部分中的这些 *.cat* 文件，并且必须在与 INF 文件相同的位置提供分发介质上的文件。 必须将 *.cat* 文件解压缩。

**注意**   如果 INF **版本** 部分不包含至少一个 **CatalogFile** 或 **CatalogFile**_xxx_ 条目，则该驱动程序将被视为无符号，并且 Windows 不显示 [**DriverVer**](inf-driverver-directive.md) 指令中列出的日期。

 

有关详细信息，请参阅 [驱动程序签名](signing-drivers-for-public-release--windows-vista-and-later-.md)。

<a name="examples"></a>示例
--------

下面的示例演示了一个简单的设备驱动程序 INF 的 **版本** 部分，后跟此示例 **版本** 部分中指定的条目所隐含的必需的 [**SourceDisksNames**](inf-sourcedisksnames-section.md)和 [**SourceDisksFiles**](inf-sourcedisksfiles-section.md)部分：

```inf
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

## <a name="see-also"></a>另请参阅


[**_DDInstall_* _](inf-ddinstall-section.md)

[_ *SourceDisksNames**](inf-sourcedisksnames-section.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**字符串**](inf-strings-section.md)

 

