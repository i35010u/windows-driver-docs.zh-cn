---
title: INF BitReg 指令
description: BitReg 指令引用一个或多个 INF 编写器定义部分用于设置或清除现有 bits [REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)-在注册表中键入值的条目。 但是，此指令很少设备/驱动程序 INF 文件中使用。
ms.assetid: d9dc601a-e0bb-488f-8bed-221ad600a88c
keywords:
- INF BitReg 指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF BitReg Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8085f27eeef0a58f253728384c831e1afd415183
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534791"
---
# <a name="inf-bitreg-directive"></a>INF BitReg 指令


**请注意**  如果要构建一个通用或移动设备的驱动程序包，此指令无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

一个**BitReg**指令引用一个或多个 INF 编写器定义部分用于设置或清除现有 bits [REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)-在注册表中键入值的条目。 但是，此指令很少设备/驱动程序 INF 文件中使用。

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


 
BitReg=bit-registry-section[,bit-registry-section]...
```

一个**BitReg**指令可以指定任何正式语法语句更高版本中所示的部分下。 此指令还可以指定任何 INF 编写器定义以下各节下：

-   一个*服务安装部分*或*事件日志安装*部分中引用[ **AddService** ](inf-addservice-directive.md)指令中DDInstall.Services 部分。
-   *添加接口部分*所引用的[ **AddInterface** ](inf-addinterface-directive.md)指令[ * **DDInstall *。接口**](inf-ddinstall-interfaces-section.md)部分。
-   *安装接口部分*中引用[ **InterfaceInstall32** ](inf-interfaceinstall32-section.md)部分

每个命名部分引用的**BitReg**指令具有以下形式：

```ini
[bit-registry-section]
reg-root, [subkey], value-entry-name, [flags], byte-mask, byte-to-modify
reg-root, [subkey], value-entry-name, [flags], byte-mask, byte-to-modify
...
```

一个*位注册表部分*可以有任意数量的条目，每个单独的行上。

## <a name="entries"></a>条目


<a href="" id="reg-root"></a>*reg-root*  
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
相对根 −，即密钥指定通过使用此缩写是相对于与此 INF 部分相关联的注册表项**BitReg**指令将出现，如下表所示。

| INF 部分包含 BitReg 指令                                    | 注册表项引用的 HKR                                                        |
|----------------------------------------------------------------------------|---------------------------------------------------------------------------------------|
| INF ***DDInstall*** |
| INF ***DDInstall *。硬件** |
| INF [ * **DDInstall *。服务**](inf-ddinstall-services-section.md)的部分 | **Services**密钥                                                                  |

 

**请注意**  **HKR**不能从 INF 引用位的注册表的部分中使用[ ***DefaultInstall*** ](inf-defaultinstall-section.md)部分。

 

有关详细信息存储在下的驱动程序信息**HKEY_LOCAL_MACHINE**根，请参阅[注册表树和设备和驱动程序的密钥](registry-trees-and-keys.md)。

<a href="" id="subkey"></a>*subkey*  
此可选值，表示为 %*strkey*中定义的 %令牌[**字符串**](inf-strings-section.md)部分的 INF 或注册表路径下给定*注册表根* (*key1\\key2\\key3*...)，指定包含要修改的值项的键。

<a href="" id="value-entry-name"></a>*value-entry-name*  
指定名称的现有[REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)-类型值条目中 （现有） 的子项以进行修改。 则可以将其表示为"*带引号的字符串*"或作为 %*strkey*INF 中定义的 %令牌[**字符串**](inf-strings-section.md)部分。

<a href="" id="flags"></a>*flags*  
此可选的十六进制值，表示为或运算的位掩码的系统定义的低位字和高位字的标志值，指定是否要清除或设置给定字节掩码中指定的位。 其默认值为零，这会清除注册表的 64 位部分中的位。

为每个这些标志的位掩码值如下所示：

<a href="" id="0x00000000--flg-bitreg-clearbits-"></a>**0x00000000** (FLG_BITREG_CLEARBITS)  
清除指定的位*字节掩码*。

<a href="" id="0x00000001--flg-bitreg-setbits-"></a>**0x00000001** (FLG_BITREG_SETBITS)  
设置由指定的位*字节掩码*。

<a href="" id="0x00004000---flg-bitreg-32bitkey--"></a>**0x00004000** (FLG_BITREG_32BITKEY)   
（Windows XP 和更高版本的 Windows。）请在 32 位注册表中指定的更改。 如果未指定，对本机注册表进行更改。

<a href="" id="byte-mask"></a>*byte-mask*  
此字节大小的掩码，以十六进制表示法中，指定要清除或中的当前值设置哪些位给定*值的条目名称*。

<a href="" id="byte-to-modify"></a>*byte-to-modify*  
此字节大小的值，用十进制，表示指定的从零开始的索引中的字节[REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)-键入要修改的值。

<a name="remarks"></a>备注
-------

每个*位注册表部分*名称必须是唯一的 INF 文件，但它可以被**BitReg**相同 INF 的其他部分中的指令。 每个 INF 编写器创建的部分名称的 INF 文件中必须是唯一和必须遵从常规规则，用于定义的节名称。 有关这些规则的详细信息，请参阅[INF 文件的常规语法规则](general-syntax-rules-for-inf-files.md)。

对现有的值[REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)-还可以通过覆盖其 INF 文件中的其他位置添加注册表部分中的当前值修改类型值项。 有关添加注册表部分的详细信息，请参阅的参考[ **AddReg**](inf-addreg-directive.md)指令。

使用**BitReg**指令需要另一个 INF 文件节的定义。 但是，对现有的值[REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)-类型值的项可以是已修改的位在此类部分中，从而保留所有剩余的位的值。

<a name="examples"></a>示例
--------

下面的示例演示的虚构应用程序位注册表部分。

```ini
[AppX_BitReg]
; set first bit of byte 0 in ProgramData value entry
HKLM,Software\AppX,ProgramData,1,0x01,0 
; preceding would change value 30,00,10 to 31,00,10

; clear high bit of byte 2 in ProgramData value entry
HKLM,Software\AppX,ProgramData,,0x80,2
; preceding would change value 30,00,f0 to 30,00,70

; set second and third bits of byte 1 in ProgramData value entry
HKLM,Software\AppX,ProgramData,1,0x06,1
; preceding would change value 30,00,f0 to 30,06,f0
```

## <a name="see-also"></a>另请参阅


[**AddInterface**](inf-addinterface-directive.md)

[**AddReg**](inf-addreg-directive.md)

[**AddService**](inf-addservice-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall*.CoInstallers**](inf-ddinstall-coinstallers-section.md)

[***DDInstall *。硬件**](inf-ddinstall-hw-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

 

 






