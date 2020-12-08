---
title: INF AddReg 指令
description: AddReg 指令将引用一个或多个 INF 写入器定义的用于修改或创建注册表信息的外接程序部分。
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
ms.openlocfilehash: fc682c2f39d008d0639ab057c5b0bdf4685bf319
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790599"
---
# <a name="inf-addreg-directive"></a>INF AddReg 指令


**AddReg** 指令将引用一个或多个 INF 写入器定义的用于修改或创建注册表信息的 *外接程序部分*。

```inf
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

每个 *添加注册表部分* 都可以有项来执行以下操作：

-   向注册表添加包含初始值项的新键。
-   向现有注册表项添加新的值项。
-   在注册表中修改特定键的现有值项。

**AddReg** 指令引用的每个命名 *的 "添加注册表" 部分* 具有以下格式：

```inf
[add-registry-section]
reg-root, [subkey],[value-entry-name],[flags],[value][,[value]]
reg-root, [subkey],[value-entry-name],[flags],[value][,[value]]
 ...
[[add-registry-section.security]
"security-descriptor-string"]
```

" *添加注册表" 部分* 可以有任意数量的条目，每个条目在单独的行中。 INF 还可以包含一个或多个可选的 " <em>添加注册表" 部分</em>**。安全** 部分，每个部分都指定一个安全描述符，应用于已命名的 " *添加注册表" 部分* 中描述的所有注册表值。

## <a name="entries"></a>项


<a href="" id="reg-root"></a>*注册表根*  
标识此项中提供的其他值的注册表树的根。 值可以是下列任一值：

<a href="" id="hkcr"></a>**HKCR**  
**HKEY_CLASSES_ROOT** 的缩写

<a href="" id="hkcu"></a>**HKCU**  
**HKEY_CURRENT_USER** 的缩写

<a href="" id="hklm"></a>**HKLM**  
**HKEY_LOCAL_MACHINE** 的缩写

<a href="" id="hku"></a>**HKU 开头**  
**HKEY_USERS** 的缩写

<a href="" id="hkr"></a>**HKR**  
相对根，其中使用此缩写指定的密钥相对于与 INF 部分关联的注册表项，其中显示了此 **AddReg** 指令，如下表所示。

| 包含 AddReg 指令的 INF 部分                        | HKR 引用的注册表项                                                        |
|----------------------------------------------------------------|---------------------------------------------------------------------------------------|
| INF [ * *_DDInstall_* _](inf-ddinstall-section.md)部分       | 设备的 _software 密钥 * |
| INF [ * **DDInstall *。HW**](inf-ddinstall-hw-section.md)部分 | 设备的 *硬件密钥* |
| INF *\[ 服务-安装节 \]* 部分                      | **服务** 密钥                                                                  |
| INF *\[ 事件日志-安装 \]* 部分                            | **EventLog** 键                                                                  |
| INF *\[ 添加接口部分 \]*                        | 设备接口的注册表项                                                    |


**请注意**，**HKR** 不能用于从 [**INF DefaultInstall 部分**](inf-defaultinstall-section.md)引用的 *添加注册表部分*。  

 

有关存储在 **HKEY_LOCAL_MACHINE** 根下的驱动程序信息的详细信息，请参阅 [设备和驱动程序的注册表树和密钥](registry-trees-and-keys.md)。

<a href="" id="subkey"></a>*键值*  
此可选值可以是在 INF 的 [**字符串**](inf-strings-section.md)部分中定义的%*strkey*% 令牌，或在给定 *的* 注册表项下作为注册表路径 (<em>key1</em> **\\** <em>key2</em> **\\** <em>key3</em>... ) ，指定以下项之一：

-   要添加到注册表中给定注册表路径末尾的新子项。
-   一个现有子项，其中写入此项中指定的其他值 (可能替换给定子项) 的现有命名值项的值。
-   新子项连同其初始值条目一起添加到注册表中。

<a href="" id="value-entry-name"></a>*值-输入名称*  
此可选值在给定 (现有) *子项* 中命名现有值条目，或者创建要添加到指定 *子项* 中的新值条目的名称，无论该名称已存在还是要添加到注册表中的新密钥。 此值可以表示为 **"**<em>带引号的字符串</em>**"** ，也可以表示为 INF 的 [**字符串**](inf-strings-section.md)部分中定义的%*strkey*% 令牌。  (如果对字符串类型的值省略此参数，则 *值输入名称* 是此项的默认 "未命名" 值项。 ) 

操作系统支持一些系统定义的特殊 *值输入* 关键字。 有关详细信息，请参阅此 **备注** 部分的结尾。

<a href="" id="flags"></a>*随意*  
此可选的十六进制值表示为系统定义的低词和高位字标志值的运算位掩码，用于定义值项的数据类型和/或控制添加注册表操作。

其中每个标志的位掩码值如下所示：

<a href="" id="0x00000001--flg-addreg-binvaluetype---"></a>**0x00000001** (FLG_ADDREG_BINVALUETYPE)    
给定值为 "原始" 数据。  (此值与 FLG_ADDREG_TYPE_BINARY 相同。 ) 

<a href="" id="0x00000002--flg-addreg-noclobber---"></a>**0x00000002** (FLG_ADDREG_NOCLOBBER)    
防止给定值替换现有值项的值。

<a href="" id="0x00000004--flg-addreg-delval-"></a>**0x00000004** (FLG_ADDREG_DELVAL)   
从注册表中删除给定的 *子项*，或从指定的注册表 *子项* 中删除指定的 *值项名称*。

<a href="" id="0x00000008--flg-addreg-append--"></a>**0x00000008** (FLG_ADDREG_APPEND)    
将给定值追加到现有的已命名值项的 *值* 。 仅当同时设置了 FLG_ADDREG_TYPE_MULTI_SZ 时，此标志才有效。 指定的字符串值如果已存在，则不追加。

<a href="" id="0x00000010--flg-addreg-keyonly-"></a>**0x00000010** (FLG_ADDREG_KEYONLY)   
创建给定的 *子项*，但忽略任何提供的值输入名称和/或值。

<a href="" id="0x00000020--flg-addreg-overwriteonly--"></a>**0x00000020** (FLG_ADDREG_OVERWRITEONLY)    
仅当指定的 *值项名称* 已存在于给定 *子项* 中时，重置为提供的 *值*。

<a href="" id="0x00001000--flg-addreg-64bitkey--"></a>**0x00001000** (FLG_ADDREG_64BITKEY)    
 (Windows XP 和更高版本的 Windows。 ) 在64位注册表中进行指定的更改。 如果未指定，则对本机注册表进行更改。

<a href="" id="0x00002000--flg-addreg-keyonly-common-"></a>**0x00002000** (FLG_ADDREG_KEYONLY_COMMON)   
 (Windows XP 和更高版本的 Windows。 ) 这与 FLG_ADDREG_KEYONLY 相同，但也适用于 [**INF DelReg 指令**](inf-delreg-directive.md)的 *del-registry 部分*。

<a href="" id="0x00004000--flg-addreg-32bitkey-"></a>**0x00004000** (FLG_ADDREG_32BITKEY)   
 (Windows XP 和更高版本的 Windows。 ) 在32位注册表中进行指定的更改。 如果未指定，则对本机注册表进行更改。

<a href="" id="0x00000000--flg-addreg-type-sz-"></a>**0x00000000** (FLG_ADDREG_TYPE_SZ)   
给定的值项和/或值的类型为 [REG_SZ](/windows/desktop/SysInfo/registry-value-types)。

**注意** 此值是指定的值项的默认类型，因此，在对此类型的值项进行操作的 "*外接* 程序" 部分中，可从任何 r 示例中的 r *示例 =* line 省略标志值。

 

<a href="" id="0x00010000--flg-addreg-type-multi-sz-"></a>**0x00010000** (FLG_ADDREG_TYPE_MULTI_SZ)   
给定的值项和/或值为注册表类型 [REG_MULTI_SZ](/windows/desktop/SysInfo/registry-value-types)。 下面的值字段可以是以逗号分隔的字符串列表。 对于给定的字符串值，此规范不需要任何 NULL 终止符。

<a href="" id="0x00020000--flg-addreg-type-expand-sz--"></a>**0x00020000** (FLG_ADDREG_TYPE_EXPAND_SZ)    
给定的 *值输入名称* 和/或 *值* 为注册表类型 [REG_EXPAND_SZ](/windows/desktop/SysInfo/registry-value-types)。

<a href="" id="0x00010001--flg-addreg-type-dword---flg-addreg-type-dword-"></a>**0x00010001** (FLG_ADDREG_TYPE_DWORD)   
给定的 *值输入名称* 和/或 *值* 为注册表类型 [REG_DWORD](/windows/desktop/SysInfo/registry-value-types)。

<a href="" id="0x00020001--flg-addreg-type-none-"></a>**0x00020001** (FLG_ADDREG_TYPE_NONE)   
给定的 *值输入名称* 和/或 *值* 为注册表类型 [REG_NONE](/windows/desktop/SysInfo/registry-value-types)。

<a href="" id="value"></a>value  
这可以选择指定要添加到给定注册表项中的指定 *值输入名称* 的新值。 此类 *值* 可以是现有键中现有命名值条目的 "替换" 值、要追加 (*标志* 值 **0x00010008**) 到现有键中的现有命名 [REG_MULTI_SZ](/windows/desktop/SysInfo/registry-value-types)类型值项、要写入现有键的新值项或要添加到注册表中的新 *子项* 的初始值条目。

此类 *值* 的表达式取决于为 *标志* 指定的注册表类型，如下所示：

-   注册表字符串类型值可以表示为 "*带引号的字符串*"，也可以表示为在 INF 文件的 [**字符串**](inf-strings-section.md)部分中定义的%*strkey*% 令牌。 此类 INF 指定的值不必在每个字符串的末尾包含 NULL 终止符。
-   注册表数值类型值可以使用0x 表示法表示为十六进制 () 或十进制数。

<a href="" id="security-descriptor-string"></a>*安全描述符-字符串*  
指定要应用于已命名的 " *添加注册表" 部分* 创建的所有注册表项的安全描述符。 *安全描述符字符串* 是包含标记的字符串，用于指示 DACL (**D：**) 安全组件。

如果未指定 "<em>添加注册表" 部分</em>，则注册表项将继承父项的安全 **设置。**

如果指定了 "<em>添加注册表" 部分</em>的 "**安全**" 部分，则必须包含以下 ACE，以便可以进行设备和系统 service pack 的安装和升级：

-    (;;GA;;;SY) −授予对本地系统的所有访问权限。
-    (;;GA;;;BA) −授予对内置管理员的所有访问权限。

不要 *指定向* 非特权用户授予写入权限的 ACE 字符串。

有关安全描述符字符串的信息，请参阅 [安全描述符定义语言 (Windows) ](/windows/desktop/SecAuthZ/security-descriptor-definition-language)。 有关安全描述符字符串的格式的信息，请参阅安全描述符定义语言 (Windows) 。

有关如何指定安全描述符的详细信息，请参阅 [创建安全设备安装](creating-secure-device-installations.md)。

<a name="remarks"></a>备注
-------

可以在上述正式语法语句中所示的任何节下指定 **AddReg** 指令。 还可以在以下任何一项由 INF 编写器定义的部分中指定此指令：

-   INF DDInstall 中的 [**AddService**](inf-addservice-directive.md)指令引用的 *服务安装部分* 或 *事件日志安装* 部分 [**。 *DDInstall* 服务部分**](inf-ddinstall-services-section.md)。
-   由 INF DDInstall 中的 [**AddInterface**](inf-addinterface-directive.md)指令引用的 *添加接口部分* [***DDInstall*。接口部分**](inf-ddinstall-interfaces-section.md)。
-   [**INF InterfaceInstall32 部分**](inf-interfaceinstall32-section.md)中引用的 *安装接口部分*。

对于 INF 文件，每个 *添加注册表部分* 名称必须是唯一的，但它可以在同一 INF 的其他部分中由 **AddReg** 指令引用。 每个节名称必须遵循用于定义 [INF 文件一般语法规则](general-syntax-rules-for-inf-files.md)中所述的部分名称的常规规则。

**注意**  标志值中的低位字的下序位区分字符和二进制数据。

 

若要表示不属于预定义的 REG_ *XXX* 类型之一的其他注册表类型，请在 *标志* 运算的高位字中指定一个新的类型号，其中 FLG_ADDREG_BINVALUETYPE 在其低字中。 此类 *值* 的数据必须以二进制格式指定为以逗号分隔的字节序列。 例如，若要存储作为值项的新注册表数据类型的16个字节的数据（如0x38），则 "添加注册表" 一节条目应如下所示：

```inf
HKR,,MYValue,0x00380001,1,0,2,3,4,5,6,7,8,9,A,B,C,D,E,F
```

此方法可用于定义数值的新注册表类型，但不能定义 [REG_EXPAND_SZ](/windows/desktop/SysInfo/registry-value-types)、 [REG_MULTI_SZ](/windows/desktop/SysInfo/registry-value-types)、 [REG_NONE](/windows/desktop/SysInfo/registry-value-types)或 [REG_SZ](/windows/desktop/SysInfo/registry-value-types)类型的值。 有关这些类型的详细信息，请参阅 [注册表值类型](/windows/desktop/SysInfo/registry-value-types)。

### <a name="special-value-entry-name-keywords"></a>特殊 *的值-输入名称* 关键字

定义了特殊关键字，以便在 HKR **AddReg** 项中使用。 使用这些关键字的条目的格式如下所示：

```inf
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

下面介绍了使用以下特殊关键字的 HKR **AddReg** 条目：

<a href="" id="devicecharacteristics"></a>**DeviceCharacteristics**  
**DeviceCharacteristics** HKR **AddReg** 项指定设备的特性。 *特性* 值是一个数值，它是 \* 在 *Ntddk 和* 中定义 *的一个* 或多个 FILE_ 文件特征值上使用或的结果。

只能在 INF 中指定以下值：

```inf
#define FILE_REMOVABLE_MEDIA            0x00000001
#define FILE_READ_ONLY_DEVICE           0x00000002
#define FILE_FLOPPY_DISKETTE            0x00000004
#define FILE_WRITE_ONCE_MEDIA           0x00000008
#define FILE_DEVICE_SECURE_OPEN         0x00000100
```

有关这些值的说明，请参阅 [**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)。

使用 **DeviceCharacteristics** 项指定的特性值将与在每次调用 **IoCreateDevice** 时指定的值运算，这些值在设备堆栈上创建设备对象。 在添加所有设备对象之后、启动设备之前，会发生或操作。

 (包括值为零) 的 *特性* 值将覆盖关联的类安装程序 INF 中指定的任何类范围的设备特性。

有关设备特征的详细信息，请参阅 [指定设备特征](../kernel/specifying-device-characteristics.md)。

<a href="" id="devicetype"></a>**DeviceType**  
**DeviceType** HKR **AddReg** 项指定设备的设备类型。 设备类型是 *Wdm* 或 *Ntddk* 中定义的 FILE_DEVICE_ *XXX* 常量的数值。 0x10001 的标志值指定设备类型值为 [REG_DWORD](/windows/desktop/SysInfo/registry-value-types)。 有关详细信息，请参阅 [指定设备类型](../kernel/specifying-device-types.md)。

类安装程序 INF 应该指定适用于类中所有设备或几乎所有设备的设备类型。 例如，如果类中的设备的类型为 FILE_DEVICE_CD_ROM，请指定一种 *设备类型* 的0x02。 如果设备 INF 为 **DeviceType** 指定了值，则它将覆盖类安装程序设置的值（如果有）。 如果类或设备 INF 指定了 **DeviceType** 值，则 PnP 管理器会将该类型应用于设备的总线驱动程序创建 *(PDO) 的物理设备对象* 。

<a href="" id="security"></a>**安全**  
**Security** HKR **AddReg** 条目指定了设备的安全描述符。 *安全描述符字符串* 是包含标记的字符串，用于指示 DACL (**D：**) 安全组件。

类安装程序 INF 可以指定设备类的安全描述符。 设备 INF 可以为单个设备指定安全描述符，替代类的安全性。 如果类和/或设备 INF 指定了一个 *安全描述符字符串*，则 PnP 管理器会将描述符传播到设备 ( *DOs*) 中的所有设备对象。 这包括函数设备对象 (*FDO*) 、可选的 *筛选器 DOs* 和 PDO。

有关安全描述符字符串的格式的信息，请参阅 Microsoft Windows SDK 文档。

有关如何指定安全描述符的详细信息，请参阅 [创建安全设备安装](creating-secure-device-installations.md)。

<a href="" id="upperfilters"></a>**UpperFilters**  
**UpperFilters** HKR **AddReg** 项指定 PnP 上层筛选器驱动程序。 DDInstall 中的此条目 [**_DDInstall_。HW**](inf-ddinstall-hw-section.md)部分定义了一个或多个特定于设备的筛选器驱动程序。 在 [**ClassInstall32**](inf-classinstall32-section.md) 节中，此项定义了一个或多个类范围的上限筛选器驱动程序。

<a href="" id="lowerfilters"></a>**LowerFilters**  
**LowerFilters** HKR **AddReg** 项指定 PnP 低筛选器驱动程序。 <em>DDInstall</em>中的此条目 **。HW 部分** 定义了一个或多个特定于设备的低筛选器驱动程序。 在 **ClassInstall32** 节中，此项定义了一个或多个类级较低的筛选器驱动程序。

<a href="" id="exclusive"></a>**异**  
如果 HKR **AddReg** 项存在并且设置为 "1" **，则它** 指定该设备是一个 *独占设备*。 否则，不会将设备视为独占设备。 有关详细信息，请参阅 [指定对设备对象的独占访问权限](../kernel/specifying-exclusive-access-to-device-objects.md)。

<a href="" id="enumproppages32"></a>**EnumPropPages32**  
**EnumPropPages32** HKR **AddReg** 项指定动态链接库的名称， (*DLL*) 文件是特定于设备的属性页提供程序。 它还指定 DLL 实现的 **ExtensionPropSheetPageProc** 回调函数的名称。 有关属性页和函数的详细信息，请参阅适用于 Windows 7 的 Microsoft Windows 软件开发工具包 (SDK) 和 .NET Framework 4.0。

**重要提示**  DLL 和 **ExtensionPropSheetPageProc** 回调函数的名称必须括在引号内 ( "" ) 。

 

<a href="" id="locationinformationoverride"></a>**LocationInformationOverride**  
 (Windows XP 和更高版本的 Windows) 可以使用 **LocationInformationOverride** HKR **AddReg** 项来指定描述设备物理位置的文本字符串。 它会重写设备的总线驱动程序为响应 [**IRP_MN_QUERY_DEVICE_TEXT**](../kernel/irp-mn-query-device-text.md)请求而提供的 **LocationInformation** 字符串。

<a href="" id="resourcepickertags"></a>**ResourcePickerTags**  
**ResourcePickerTags** HKR **AddReg** 项指定设备的资源选取器标记。

<a href="" id="resourcepickerexceptions"></a>**ResourcePickerExceptions**  
**ResourcePickerExceptions** HKR **AddReg** 项指定设备允许的资源冲突。

<a name="examples"></a>示例
--------

在此示例中， **AddReg** 指令引用 Miniport_EventLog_AddReg)  (了 <em>DDInstall</em>中 **ADDSERVICE** 指令引用的由 INF 编写器定义的部分 **。服务** 部分。

```inf
[Miniport_EventLog_AddReg]
HKR,,EventMessageFile,0x00020000,"%%SystemRoot%%\System32\IoLogMsg.dll" 
; double quotation marks delimiters in preceding entry prevent truncation 
; if line wraps
 
HKR,,TypesSupported,0x00010001,7 
```

请注意，可以指定十六进制格式的标志值（如示例中所示），也可以定义字符串占位符，如 `%FLG_ADDREG_TYPE_DWORD%` 每个 INF 文件的 [字符串] 部分。

## <a name="see-also"></a>请参阅


[**AddInterface**](inf-addinterface-directive.md)

[**AddService**](inf-addservice-directive.md)

[**BitReg**](inf-bitreg-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[**_DDInstall_* _](inf-ddinstall-section.md)

[_ *_DDInstall_。CoInstallers**](inf-ddinstall-coinstallers-section.md)

[**_DDInstall_。HW**](inf-ddinstall-hw-section.md)

[**_DDInstall_。接口**](inf-ddinstall-interfaces-section.md)

[**_DDInstall_。服务器**](inf-ddinstall-services-section.md)

[**DelReg**](inf-delreg-directive.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**字符串**](inf-strings-section.md)

 

