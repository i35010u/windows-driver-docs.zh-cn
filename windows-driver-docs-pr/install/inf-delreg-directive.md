---
title: INF DelReg 指令
description: DelReg 指令将引用一个或多个由 INF 编写器定义的部分，这些部分描述要从注册表中删除的项和/或值项。
keywords:
- INF DelReg 指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF DelReg Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc664d74613ad820c899cfc307b623d8c7284733
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813141"
---
# <a name="inf-delreg-directive"></a>INF DelReg 指令


**注意**  如果要构建通用或移动驱动程序包，则此指令无效。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

**DelReg** 指令将引用一个或多个由 INF 编写器定义的部分，这些部分描述要从注册表中删除的项和/或值项。

```inf
[DDInstall] | 
[DDInstall.CoInstallers] | 
[ClassInstall32] | 
[ClassInstall32.ntx86] | 
[ClassInstall32.ntia64] |  (Windows XP and later versions of Windows)
[ClassInstall32.ntamd64]  (Windows XP and later versions of Windows)
[ClassInstall32.ntarm]  (Windows 8 and later versions of Windows)
[ClassInstall32.ntarm64]  (Windows 10 and later versions of Windows)

 
DelReg=del-registry-section[,del-registry-section]...
```

**DelReg** 指令引用的每个 *del-registry 部分* 都具有以下格式：

```inf
[del-registry-section]
reg-root-string,subkey[,value-entry-name][,flags][,value]
reg-root-string,subkey[,value-entry-name][,flags][,value]
...
```

*Del-registry 部分* 可以有任意数量的条目，每个条目在单独的行中。

## <a name="entries"></a>项


<a href="" id="reg-root-string"></a>*.reg-字符串*  
标识此项中提供的其他值的注册表树的根。 值可以是下列任一值：

<a href="" id="hkcr"></a>**HKCR**  
**HKEY_CLASSES_ROOT** 的缩写。

<a href="" id="hkcu"></a>**HKCU**  
**HKEY_CURRENT_USER** 的缩写。

<a href="" id="hklm"></a>**HKLM**  
**HKEY_LOCAL_MACHINE** 的缩写。

<a href="" id="hku"></a>**HKU 开头**  
**HKEY_USERS** 的缩写。

<a href="" id="hkr"></a>**HKR**  
相对根，其中使用此缩写指定的密钥相对于与 INF 部分关联的注册表项，其中显示了此 **DelReg** 指令，如下表所示。

| 包含 AddReg 指令的 NF-E 部分                                     | HKR 引用的注册表项                                                        |
|----------------------------------------------------------------------------|---------------------------------------------------------------------------------------|
| INF [ * *_DDInstall_* _](inf-ddinstall-section.md)部分                   | 设备的 _software 密钥 * |
| INF [ * **DDInstall *。HW**](inf-ddinstall-hw-section.md)部分             | 设备的 *硬件密钥* |
| INF [ * **DDInstall *。服务**](inf-ddinstall-services-section.md)部分 | **服务** 密钥                                                                  |

 

**请注意**，不能在从 [**INF DefaultInstall 部分**](inf-defaultinstall-section.md)引用的 **HKR** *部分* 中使用。  

 

有关存储在 **HKEY_LOCAL_MACHINE** 根下的驱动程序信息的详细信息，请参阅 [设备和驱动程序的注册表树和密钥](registry-trees-and-keys.md)。

<a href="" id="subkey"></a>*键值*  
此可选值可以是在 INF 的 [**字符串**](inf-strings-section.md)部分中定义的%*strkey*% 令牌，或在给定 *的* 注册表项下作为注册表路径 (<em>key1</em> **\\** <em>key2</em> **\\** <em>key3</em>... ) ，指定以下项之一：

-   要从注册表的给定注册表路径末尾删除的子项
-   要从中删除给定的值项名称的现有子项

<a href="" id="value-entry-name"></a>*值-输入名称*  
此值标识要从给定子项中移除的命名值项。 如果要从注册表中删除子项本身，则应该省略此值及其前面的逗号。

<a href="" id="flags"></a>*随意*  
 (Windows XP 和更高版本的 Windows。 ) 此可选的十六进制值，表示为系统定义的低词和高位字标志值的运算位掩码，用于定义值项的数据类型，或控制删除注册表操作。 如果未指定 *flags* ，则 (将删除指定) 或 *子项* 时的 *值输入名称*。

其中每个标志的位掩码值如下所示：

<a href="" id="0x00002000--flg-delreg-keyonly-common---"></a>**0x00002000** (FLG_DELREG_KEYONLY_COMMON)    
删除整个子项。

<a href="" id="0x00004000---flg-delreg-32bitkey-"></a>**0x00004000** (FLG_DELREG_32BITKEY)   
在32位注册表中进行指定的更改。 如果未指定，则对本机注册表进行更改。

<a href="" id="0x00018002--flg-delreg-multi-sz-delstring-"></a>**0x00018002** (FLG_DELREG_MULTI_SZ_DELSTRING)   
在多字符串注册表项中，删除与值指定的字符串值匹配的所有字符串。 忽略大小写。

<a href="" id="value"></a>value  
 (Windows XP 和更高版本的 Windows。 ) 指定注册表值（如果 *flags* 表明需要注册表值）。

<a name="remarks"></a>备注
-------

可以在上述正式语法语句中所示的任何节下指定 **DelReg** 指令。 还可以在以下任何一项由 INF 编写器定义的部分中指定此指令：

-   INF DDInstall 中的 [**AddService**](inf-addservice-directive.md)指令引用的 *服务安装部分* 或 *事件日志安装* 部分 [**。 *DDInstall* 服务部分**](inf-ddinstall-services-section.md)。
-   由 INF DDInstall 中的 [**AddInterface**](inf-addinterface-directive.md)指令引用的 *添加接口部分* [***DDInstall*。接口部分**](inf-ddinstall-interfaces-section.md)。
-   [**INF InterfaceInstall32 部分**](inf-interfaceinstall32-section.md)中引用的 *安装接口部分*。

通常，INF 决不会尝试删除由系统组件或 INF 文件为其他设备设置的子项或现有子项内的值项。 *删除注册表部分* 的目的是使用同一个提供程序提供的新 INF 文件，从以前的安装中清除过时的注册表信息。

对于 INF 文件，每个 *del-registry 节* 名称必须是唯一的，但它可以在同一 INF 的其他部分中通过 **DelReg** 指令进行引用。 每个节名称必须遵循用于定义节名称的常规规则。 有关这些规则的详细信息，请参阅 [INF 文件的一般语法规则](general-syntax-rules-for-inf-files.md)。

使用 Windows XP 之前的操作系统版本，删除密钥的唯一方法是指定以下各项：

```inf
reg-root-string, subkey
```

对于 Windows XP 和更高版本的 Windows，还允许 (指定32位注册表) ：

```inf
reg-root-string, subkey,,0x4000
```

<a name="examples"></a>示例
--------

此示例显示系统提供的 COM/LPT 端口类安装程序的 INF 如何从注册表中删除有关 COM 端口的过时特定于 NT 的注册表信息。

```inf
[ComPort.NT]
CopyFiles=ComPort.NT.Copy
AddReg=ComPort.AddReg, ComPort.NT.AddReg
 ... ; more directives omitted here

[ComPort.NT.HW]
DelReg=ComPort.NT.HW.DelReg

[ComPort.NT.Copy]
serial.sys
serenum.sys

[Comport.NT.AddReg]
HKR,,EnumPropPages32,,"MSPorts.dll,SerialPortPropPageProvider"

[ComPort.NT.HW.DelReg]
HKR,,UpperFilters
```

## <a name="see-also"></a>请参阅


[**AddReg**](inf-addreg-directive.md)

[**AddInterface**](inf-addinterface-directive.md)

[**AddService**](inf-addservice-directive.md)

[**BitReg**](inf-bitreg-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[**_DDInstall_* _](inf-ddinstall-section.md)

[_ *_DDInstall_。CoInstallers**](inf-ddinstall-coinstallers-section.md)

[**_DDInstall_。HW**](inf-ddinstall-hw-section.md)

[**_DDInstall_。服务器**](inf-ddinstall-services-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**字符串**](inf-strings-section.md)

 

 






