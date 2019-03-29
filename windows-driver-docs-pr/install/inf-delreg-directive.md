---
title: INF DelReg 指令
description: DelReg 指令引用一个或多个 INF 编写器定义各节描述密钥和/或值项来从注册表中删除。
ms.assetid: a456327f-9b2c-42e6-a575-47ad788aa8b1
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
ms.openlocfilehash: fbde52ab47f5eb3f99f5f3bf83103c674125d41a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577182"
---
# <a name="inf-delreg-directive"></a>INF DelReg 指令


**请注意**  如果要构建一个通用或移动设备的驱动程序包，此指令无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

一个**DelReg**指令引用一个或多个 INF 编写器定义各节描述密钥和/或值项来从注册表中删除。

```ini
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

每个*del 注册表部分*所引用的**DelReg**指令具有以下形式：

```ini
[del-registry-section]
reg-root-string,subkey[,value-entry-name][,flags][,value]
reg-root-string,subkey[,value-entry-name][,flags][,value]
...
```

一个*del 注册表部分*可以有任意数量的条目，每个单独的行上。

## <a name="entries"></a>条目


<a href="" id="reg-root-string"></a>*reg-root-string*  
标识在此条目中提供的其他值的注册表树的根。 该值可以是下列值之一：

<a href="" id="hkcr"></a>**HKCR**  
缩写**HKEY_CLASSES_ROOT**。

<a href="" id="hkcu"></a>**HKCU**  
缩写**HKEY_CURRENT_USER**。

<a href="" id="hklm"></a>**HKLM**  
缩写**HKEY_LOCAL_MACHINE**。

<a href="" id="hku"></a>**HKU**  
缩写**HKEY_USERS**。

<a href="" id="hkr"></a>**HKR**  
在其中使用此缩写指定的键是相对于与此 INF 部分相关联的注册表项的相对根**DelReg**指令将出现，如下表所示。

| NF 部分包含 AddReg 指令                                     | 注册表项引用的 HKR                                                        |
|----------------------------------------------------------------------------|---------------------------------------------------------------------------------------|
| INF ***DDInstall*** |
| INF ***DDInstall *。硬件** |
| INF [ * **DDInstall *。服务**](inf-ddinstall-services-section.md)部分 | **Services**密钥                                                                  |

 

**请注意**  **HKR**不能用于*del 注册表部分*引用从[ **INF DefaultInstall 部分**](inf-defaultinstall-section.md)。

 

有关详细信息存储在下的驱动程序信息**HKEY_LOCAL_MACHINE**根，请参阅[注册表树和设备和驱动程序的密钥](registry-trees-and-keys.md)。

<a href="" id="subkey"></a>*subkey*  
此可选值，格式为 %*strkey*中定义的 %令牌[**字符串**](inf-strings-section.md)部分的 INF 或注册表路径下给定*reg 根*(<em>key1</em>**\\**<em>key2</em>**\\**<em>key3</em>...)，指定以下值之一：

-   若要从注册表中的给定的注册表路径的末尾删除一个子项
-   从该给定的值的项名称是要删除一个现有子项

<a href="" id="value-entry-name"></a>*value-entry-name*  
此值标识要从给定的子项中删除的命名的值项。 如果正在从注册表中删除的子项本身，应省略此值和其前面的逗号。

<a href="" id="flags"></a>*flags*  
（Windows XP 和更高版本的 Windows。）此可选十六进制值，表示为或运算的位掩码的系统定义的低位字和高位字标志值，定义一个值项的数据类型，也控制删除注册表操作。 如果*标志*未指定，则*值条目名称*（如果指定） 或*子项*将被删除。

为每个这些标志的位掩码值如下所示：

<a href="" id="0x00002000--flg-delreg-keyonly-common---"></a>**0x00002000** (FLG_DELREG_KEYONLY_COMMON)   
删除整个子项。

<a href="" id="0x00004000---flg-delreg-32bitkey-"></a>**0x00004000** (FLG_DELREG_32BITKEY)  
请在 32 位注册表中指定的更改。 如果未指定，对本机注册表进行更改。

<a href="" id="0x00018002--flg-delreg-multi-sz-delstring-"></a>**0x00018002** (FLG_DELREG_MULTI_SZ_DELSTRING)  
一个多字符串注册表项中删除所有匹配的值指定一个字符串值的字符串。 忽略大小写。

<a href="" id="value"></a>*value*  
（Windows XP 和更高版本的 Windows。）指定的注册表值，如果*标志*表示需要注册表值。

<a name="remarks"></a>备注
-------

一个**DelReg**指令可以指定任何正式语法语句更高版本中所示的部分下。 此指令还可以指定任何 INF 编写器定义以下各节下：

-   一个*服务安装部分*或*事件日志安装*部分中引用[ **AddService** ](inf-addservice-directive.md)指令[ **INF *DDInstall*。服务部分**](inf-ddinstall-services-section.md)。
-   *添加接口部分*所引用的[ **AddInterface** ](inf-addinterface-directive.md)指令[ **INF *DDInstall*.接口部分**](inf-ddinstall-interfaces-section.md)。
-   *安装接口部分*中引用[ **INF InterfaceInstall32 部分**](inf-interfaceinstall32-section.md)。

一般情况下，INF 应该永远不会尝试删除子项或值项中已设置，系统组件或其他设备的 INF 文件的现有子项。 目的*删除注册表部分*是通过使用新的 INF 文件提供的相同的提供程序清理先前安装中的旧注册信息。

每个*del 注册表部分*名称必须是唯一的 INF 文件，但它可以被**DelReg**相同 INF 的其他部分中的指令。 每个节名必须遵循的一般规则用于定义的节名称。 有关这些规则的详细信息，请参阅[INF 文件的常规语法规则](general-syntax-rules-for-inf-files.md)。

与 Windows XP 之前的操作系统版本，若要删除某一项的唯一方法是通过指定以下：

```ini
reg-root-string, subkey
```

对于 Windows XP 和更高版本的 Windows，以下还允许 （指定 32 位注册表）：

```ini
reg-root-string, subkey,,0x4000
```

<a name="examples"></a>示例
--------

此示例演示如何系统提供 COM/LPT 端口类安装程序的 INF 删除过时 NT 注册表有关特定的信息从注册表的 COM 端口。

```ini
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

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall*.CoInstallers**](inf-ddinstall-coinstallers-section.md)

[***DDInstall *。硬件**](inf-ddinstall-hw-section.md)

[***DDInstall*.Services**](inf-ddinstall-services-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**Strings**](inf-strings-section.md)

 

 






