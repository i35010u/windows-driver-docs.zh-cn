---
title: INF AddReg 指令
description: AddReg 指令引用一个或多个 INF 编写器定义添加的注册表-部分用于修改或创建注册表信息。
ms.assetid: e8162e20-0d8c-4400-9f4d-5f4abe81305b
keywords:
- INF AddReg 指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF AddReg Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88c7e40ac8401e490da57a30dee3f526c1ea938a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385928"
---
# <a name="inf-addreg-directive"></a>INF AddReg 指令


**AddReg**指令引用了一个或多 INF 编写器的定义*添加注册表部分*，用于修改或创建注册表信息。

```ini
[DDInstall] | 
[DDInstall.HW] | 
[DDInstall.CoInstallers] | 
[ClassInstall32] | 
[ClassInstall32.ntx86] | 
[ClassInstall32.ntia64] |  (Windows XP and later versions of Windows)
[ClassInstall32.ntamd64]  (Windows XP and later versions of Windows) 
[ClassInstall32.ntarm]  (Windows 8 and later versions of Windows) 
[ClassInstall32.ntarm64]  (Windows 10 and later versions of Windows) 


[install-interface-section] | 
[service-install-section] | 
[event-log-install] | 
[add-interface-section]
AddReg=add-registry-section[,add-registry-section] ...
```

每个*添加注册表部分*可以有条目以执行以下操作：

-   将新的密钥，也可能包含初始值条目添加到注册表。
-   将新值项添加到现有的注册表项。
-   修改注册表中的特定项的现有值的项。

每个名为*添加注册表部分*所引用的**AddReg**指令具有以下格式：

```ini
[add-registry-section]
reg-root, [subkey],[value-entry-name],[flags],[value][,[value]]
reg-root, [subkey],[value-entry-name],[flags],[value][,[value]]
 ...
[[add-registry-section.security]
"security-descriptor-string"]
```

*添加注册表部分*可以有任意数量的条目，每个单独的行上。 INF 还可以包含一个或多个可选<em>添加注册表部分</em>**安全**部分，每个指定的安全描述符应用到命名中所述的所有注册表值*添加注册表部分*。

## <a name="entries"></a>条目


<a href="" id="reg-root"></a>*reg-root*  
标识在此条目中提供的其他值的注册表树的根。 该值可以是下列值之一：

<a href="" id="hkcr"></a>**HKCR**  
缩写词**HKEY_CLASSES_ROOT**

<a href="" id="hkcu"></a>**HKCU**  
缩写词**HKEY_CURRENT_USER**

<a href="" id="hklm"></a>**HKLM**  
缩写词**HKEY_LOCAL_MACHINE**

<a href="" id="hku"></a>**HKU**  
缩写词**HKEY_USERS**

<a href="" id="hkr"></a>**HKR**  
在其中使用此缩写指定的键是相对于与此 INF 部分相关联的注册表项的相对根**AddReg**指令将出现，如下表所示。

| INF 部分包含 AddReg 指令                        | 注册表项引用的 HKR                                                        |
|----------------------------------------------------------------|---------------------------------------------------------------------------------------|
| INF ***DDInstall*** |
| INF ***DDInstall *。硬件** |
| INF *\[服务安装部分\]* 部分                      | **Services**密钥                                                                  |
| INF *\[事件日志安装\]* 部分                            | **EventLog**密钥                                                                  |
| INF *\[添加接口部分\]* 部分                        | 设备接口的注册表项                                                    |


**请注意**  **HKR**不能用于*添加注册表部分*引用从[ **INF DefaultInstall 部分**](inf-defaultinstall-section.md)。

 

有关详细信息存储在下的驱动程序信息**HKEY_LOCAL_MACHINE**根，请参阅[注册表树和设备和驱动程序的密钥](registry-trees-and-keys.md)。

<a href="" id="subkey"></a>*subkey*  
此可选值，格式为 %*strkey*中定义的 %令牌[**字符串**](inf-strings-section.md)部分的 INF 或注册表路径下给定*reg 根*(<em>key1</em> **\\** <em>key2</em> **\\** <em>key3</em>...)，指定以下值之一：

-   若要添加到注册表中给定的注册表路径的末尾的一个新子项。
-   此条目中指定的其他值写入 （可能替换给定的子项的现有已命名的值条目的值） 在其中一个现有子项。
-   这两个新子项添加到其初始值条目以及注册表。

<a href="" id="value-entry-name"></a>*value-entry-name*  
此可选值要么名称中给定 （现有） 的现有值条目*子项*或创建要添加的新值项的名称中指定*子项*，无论它已存在或为新的密钥要添加到注册表。 此值可以表示为 **"** <em>带引号的字符串</em> **"** 或作为 %*strkey*INF 中定义的 %令牌[**字符串**](inf-strings-section.md)部分。 (如果这字符串类型的值，省略*值的条目名称*是默认值"未命名的"值输入此密钥。)

操作系统支持一些系统定义的特殊*值的条目名称*关键字。 请参阅此实例的末尾**备注**部分，了解详细信息。

<a href="" id="flags"></a>*flags*  
此可选十六进制值，表示为的系统定义的低位字和高位字标志或运算的位掩码值、 定义值项的数据类型和/或控制添加注册表操作。

为每个这些标志的位掩码值如下所示：

<a href="" id="0x00000001--flg-addreg-binvaluetype---"></a>**0x00000001** (FLG_ADDREG_BINVALUETYPE)   
给定的值为"原始"数据。 （此值等同于 FLG_ADDREG_TYPE_BINARY。）

<a href="" id="0x00000002--flg-addreg-noclobber---"></a>**0x00000002** (FLG_ADDREG_NOCLOBBER)   
将现有值项的值替换为阻止给定的值。

<a href="" id="0x00000004--flg-addreg-delval-"></a>**0x00000004** (FLG_ADDREG_DELVAL)  
删除给定*子项*从注册表中或删除指定*值条目名称*从指定的注册表*子项*。

<a href="" id="0x00000008--flg-addreg-append--"></a>**0x00000008** (FLG_ADDREG_APPEND)   
追加给定*值*与命名的值的某个现有条目。 此标志为 FLG_ADDREG_TYPE_MULTI_SZ 还设置才有效。 如果已存在，不会追加指定的字符串值。

<a href="" id="0x00000010--flg-addreg-keyonly-"></a>**0x00000010** (FLG_ADDREG_KEYONLY)  
创建给定*子项*，但忽略任何提供的值的条目的名称和/或值。

<a href="" id="0x00000020--flg-addreg-overwriteonly--"></a>**0x00000020** (FLG_ADDREG_OVERWRITEONLY)   
重置为所提供*值*仅当指定*值条目名称*中已存在给定*子项*。

<a href="" id="0x00001000--flg-addreg-64bitkey--"></a>**0x00001000** (FLG_ADDREG_64BITKEY)   
（Windows XP 和更高版本的 Windows。）请在 64 位注册表中指定的更改。 如果未指定，对本机注册表进行更改。

<a href="" id="0x00002000--flg-addreg-keyonly-common-"></a>**0x00002000** (FLG_ADDREG_KEYONLY_COMMON)  
（Windows XP 和更高版本的 Windows。）这是与 FLG_ADDREG_KEYONLY 相同，但也适用于在*del 注册表部分*的[ **INF DelReg 指令**](inf-delreg-directive.md)。

<a href="" id="0x00004000--flg-addreg-32bitkey-"></a>**0x00004000** (FLG_ADDREG_32BITKEY)  
（Windows XP 和更高版本的 Windows。）请在 32 位注册表中指定的更改。 如果未指定，对本机注册表进行更改。

<a href="" id="0x00000000--flg-addreg-type-sz-"></a>**0x00000000** (FLG_ADDREG_TYPE_SZ)  
给定的值项和/或值属于类型[REG_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)。

**请注意**  此值是一个指定的值项的默认类型，因此可以从任何 r 省略标志值*例如根 =* 中一行*添加注册表部分*，让其运行上此类型的值项。

 

<a href="" id="0x00010000--flg-addreg-type-multi-sz-"></a>**0x00010000** (FLG_ADDREG_TYPE_MULTI_SZ)  
给定的值项和/或值的注册表类型是[REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)。 下面的值字段可以是一系列由逗号分隔的字符串。 对于给定的字符串值，此规范不要求任何 NULL 终止符。

<a href="" id="0x00020000--flg-addreg-type-expand-sz--"></a>**0x00020000** (FLG_ADDREG_TYPE_EXPAND_SZ)   
给定*值的条目名称*和/或*值*的注册表类型[REG_EXPAND_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)。

<a href="" id="0x00010001--flg-addreg-type-dword---flg-addreg-type-dword-"></a>**0x00010001** (FLG_ADDREG_TYPE_DWORD) (FLG_ADDREG_TYPE_DWORD)  
给定*值的条目名称*和/或*值*的注册表类型[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)。

<a href="" id="0x00020001--flg-addreg-type-none-"></a>**0x00020001** (FLG_ADDREG_TYPE_NONE)  
给定*值的条目名称*和/或*值*的注册表类型[REG_NONE](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)。

<a href="" id="value"></a>*value*  
这还可以指定新值来指定*值的条目名称*要添加到给定的注册表项。 此类*值*对于现有的已命名值条目中的现有密钥，要追加的值可以是"替换"值 (*标志*值**0x00010008**) 到现有的名为[REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)的现有密钥、 新值条目写入到现有的密钥或初始值条目中的一个新类型值条目*子项*若要添加到注册表。

此类表达式*值*取决于为指定的注册表类型*标志*，按如下所示：

-   注册表字符串类型值可以表示为"*带引号的字符串*"或作为 %*strkey*中定义的 %令牌[**字符串**](inf-strings-section.md)部分INF 文件中。 INF 指定值不需要包括 NULL 终止符的每个字符串的末尾。
-   注册表数值类型值可以表示为 （通过使用 0 x 表示法） 的十六进制或十进制数。

<a href="" id="security-descriptor-string"></a>*security-descriptor-string*  
指定要应用于创建的名为的所有注册表项的安全描述符*添加注册表部分*。 *安全描述符字符串*是标记，则指示 DACL 的字符串 (**d:** ) 安全组件。

如果<em>添加注册表部分</em>**安全**部分未指定，则注册表项继承父项的安全设置。

如果<em>添加注册表部分</em>**安全**指定部分，以便进行安装和升级的设备和系统服务包必须包含以下 ACE:

-   (A;GA;;SY) − 授予对本地系统的所有访问。
-   (A;GA;;BA) − 向内置管理员授予的所有访问。

不要*不*指定对非特权用户授予写入权限的 ACE 字符串。

有关安全描述符字符串的信息，请参阅[安全描述符定义语言 (Windows)](https://docs.microsoft.com/windows/desktop/SecAuthZ/security-descriptor-definition-language)。 有关的安全描述符字符串格式的信息，请参阅安全描述符定义语言 (Windows)。

有关如何指定安全描述符的详细信息，请参阅[创建安全的设备安装](creating-secure-device-installations.md)。

<a name="remarks"></a>备注
-------

**AddReg**指令可以指定任何正式语法语句更高版本中所示的部分下。 此指令还可以指定任何 INF 编写器定义以下各节下：

-   一个*服务安装部分*或*事件日志安装*部分中引用[ **AddService** ](inf-addservice-directive.md)指令[ **INF *DDInstall*。服务部分**](inf-ddinstall-services-section.md)。
-   *添加接口部分*所引用的[ **AddInterface** ](inf-addinterface-directive.md)指令[ **INF *DDInstall*.接口部分**](inf-ddinstall-interfaces-section.md)。
-   *安装接口部分*中引用[ **INF InterfaceInstall32 部分**](inf-interfaceinstall32-section.md)。

每个*添加注册表部分*名称必须是唯一的 INF 文件，但它可以被**AddReg**相同 INF 的其他部分中的指令。 每个节名必须遵循的一般规则，定义的节名称中所述[INF 文件的常规语法规则](general-syntax-rules-for-inf-files.md)。

**请注意**  标志值中的低位字的较低顺序位区分字符和二进制数据。

 

若要表示的注册表类型以外的预定义 REG_*XXX*类型，指定新类型的数字的高位字中*标志*FLG_ADDREG_BINVALUETYPE 低位字在与或运算。 此类的数据*值*必须以二进制格式指定为逗号分隔的字节序列。 例如，若要将 16 个字节的新的注册表数据类型，如 0x38，数据存储为值项，添加注册表部分条目将类似于以下内容：

```ini
HKR,,MYValue,0x00380001,1,0,2,3,4,5,6,7,8,9,A,B,C,D,E,F
```

此方法可以用于定义新的注册表类型为数值，而不是类型的值[REG_EXPAND_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)， [REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)， [REG_NONE](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)，或者[REG_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)。 有关这些类型的详细信息，请参阅[注册表值类型](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)。

### <a name="special-value-entry-name-keywords"></a>特殊*值的条目名称*关键字

特殊关键字定义用于 HKR **AddReg**条目。 使用这些关键字的项的格式如下所示：

```ini
[HKR,,DeviceCharacteristics,0x10001,characteristics] 
[HKR,,DeviceType,0x10001,device-type] 
[HKR,,Security,,security-descriptor-string] 
[HKR,,UpperFilters,0x10000,service-name] 
[HKR,,LowerFilters,0x10000,service-name] 
[HKR,,Exclusive,0x10001,exclusive-device] 
[HKR,,EnumPropPages32,,"prop-provider.dll,provider-entry-point"]
[HKR,,LocationInformationOverride,,"text-string"] 
[HKR,,ResourcePickerTags,,"text-string"] 
[HKR,,ResourcePickerExceptions,,"text-string"] ,
```

下面介绍 HKR **AddReg**使用这些特殊关键字的条目：

<a href="" id="devicecharacteristics"></a>**DeviceCharacteristics**  
一个**DeviceCharacteristics** HKR **AddReg**条目指定设备的特征。 *特征*值是数字值的结果的使用，或者在一个或多个 FILE_\*文件中定义的特性值*wdm.h 中*和*Ntddk.h*.

INF 中，可以指定只有以下值：

```ini
#define FILE_REMOVABLE_MEDIA            0x00000001
#define FILE_READ_ONLY_DEVICE           0x00000002
#define FILE_FLOPPY_DISKETTE            0x00000004
#define FILE_WRITE_ONCE_MEDIA           0x00000008
#define FILE_DEVICE_SECURE_OPEN         0x00000100
```

有关这些值的说明，请参阅[ **IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)。

通过使用指定的特性值**DeviceCharacteristics**条目，每次调用中指定的是或运算**IoCreateDevice**设备堆栈上创建一个设备对象。 添加设备的所有对象之后，但启动设备之前，将发生或运算。

*特征*（包括值为零） 的值将重写关联的类安装程序 INF 中指定的任何类范围内的设备特征。

有关设备特征的详细信息，请参阅[指定设备特征](https://docs.microsoft.com/windows-hardware/drivers/kernel/specifying-device-characteristics)。

<a href="" id="devicetype"></a>**DeviceType**  
一个**DeviceType** HKR **AddReg**条目指定设备的设备类型。 设备类型是数字值的 FILE_DEVICE_*XXX*中定义常量*wdm.h 中*或*Ntddk.h*。 0x10001 的标志值指定的设备类型值都[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)。 有关详细信息，请参阅[指定设备类型](https://docs.microsoft.com/windows-hardware/drivers/kernel/specifying-device-types)。

类 installer INF 应指定适用于所有，或几乎所有的类中的设备的设备类型。 例如，如果在类中的设备的类型 FILE_DEVICE_CD_ROM，指定*设备类型*的 0x02。 如果设备 INF 中指定的值**DeviceType**，它将替代类安装程序中，设置的值，如果有的话。 如果指定了类或设备 INF **DeviceType**值，即插即用管理器应用到该类型*物理设备对象 (PDO)* 创建的设备的总线驱动程序。

<a href="" id="security"></a>**安全**  
一个**安全**HKR **AddReg**条目指定设备的安全描述符。 *安全描述符字符串*是标记，则指示 DACL 的字符串 (**d:** ) 安全组件。

类 installer INF 可以指定设备类的安全描述符。 设备 INF 可以指定单个设备，重写类的安全性的安全描述符。 如果指定了类和/或设备 INF*安全描述符字符串*，即插即用管理器将传播到所有设备对象的描述符 ( *DOs*) 设备。 这包括函数设备对象 (*FDO*)、 可选*筛选 DOs*，和 PDO。

有关的安全描述符字符串格式的信息，请参阅 Microsoft Windows SDK 文档。

有关如何指定安全描述符的详细信息，请参阅[创建安全的设备安装](creating-secure-device-installations.md)。

<a href="" id="upperfilters"></a>**UpperFilters**  
**上边的筛选程序**HKR **AddReg**条目指定的即插即用的上限筛选器驱动程序。 中的此条目[ * **DDInstall *。HW** ](inf-ddinstall-hw-section.md)部分定义了一个或多个特定于设备的上限筛选器驱动程序。 在中[ **ClassInstall32** ](inf-classinstall32-section.md)部分中，此项定义一个或多个类范围上限筛选器驱动程序。

<a href="" id="lowerfilters"></a>**下边的筛选程序**  
一个**下边的筛选程序**HKR **AddReg**条目指定即插即用的较低的筛选器驱动程序。 中的此条目<em>DDInstall</em> **。硬件部分**定义一个或多个特定于设备的较低的筛选器驱动程序。 在中**ClassInstall32**部分中，此项定义一个或多个类范围低筛选器驱动程序。

<a href="" id="exclusive"></a>**Exclusive**  
**独占**HKR **AddReg**项，如果它存在并且设置为"1"，指定该设备是否*独占设备*。 否则该设备不被视为为排他。 有关详细信息，请参阅[指定对设备对象的独占访问](https://docs.microsoft.com/windows-hardware/drivers/kernel/specifying-exclusive-access-to-device-objects)。

<a href="" id="enumproppages32"></a>**EnumPropPages32**  
**EnumPropPages32** HKR **AddReg**条目指定的动态链接库的名称 (*DLL*) 是特定于设备的属性页提供程序的文件。 它还指定的名称**ExtensionPropSheetPageProc**由 DLL 实现回调函数。 有关属性页和函数的详细信息，请参阅适用于 Windows 7 和.NET Framework 4.0 的 Microsoft Windows 软件开发工具包 (SDK)。

**重要**  这两个 DLL 的名称和**ExtensionPropSheetPageProc**回调函数一起必须用引号 ("")。

 

<a href="" id="locationinformationoverride"></a>**LocationInformationOverride**  
（Windows XP 和更高版本的 Windows）一个**LocationInformationOverride** HKR **AddReg**条目可以用于指定一个文本字符串，描述设备的物理位置。 它将替代**LocationInformation**设备的总线驱动程序在响应中提供的字符串[ **IRP_MN_QUERY_DEVICE_TEXT** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-text)请求。

<a href="" id="resourcepickertags"></a>**ResourcePickerTags**  
一个**ResourcePickerTags** HKR **AddReg**条目指定的设备资源选取器标记。

<a href="" id="resourcepickerexceptions"></a>**ResourcePickerExceptions**  
一个**ResourcePickerExceptions** HKR **AddReg**项指定了允许的设备的资源冲突。

<a name="examples"></a>示例
--------

**AddReg**指令引用在此示例中，引用的 INF 编写器定义部分下的 (SCSI) Miniport_EventLog_AddReg 部分**AddService**指令<em>DDInstall</em> **。服务**此 INF 部分。

```ini
[Miniport_EventLog_AddReg]
HKR,,EventMessageFile,0x00020000,"%%SystemRoot%%\System32\IoLogMsg.dll" 
; double quotation marks delimiters in preceding entry prevent truncation 
; if line wraps
 
HKR,,TypesSupported,0x00010001,7 
```

## <a name="see-also"></a>请参阅


[**AddInterface**](inf-addinterface-directive.md)

[**AddService**](inf-addservice-directive.md)

[**BitReg**](inf-bitreg-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall*.CoInstallers**](inf-ddinstall-coinstallers-section.md)

[***DDInstall *。硬件**](inf-ddinstall-hw-section.md)

[***DDInstall *。接口**](inf-ddinstall-interfaces-section.md)

[***DDInstall*.Services**](inf-ddinstall-services-section.md)

[**DelReg**](inf-delreg-directive.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**Strings**](inf-strings-section.md)

 

 






