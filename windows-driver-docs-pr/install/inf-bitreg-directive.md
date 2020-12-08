---
title: INF BitReg 指令
description: BitReg 指令引用一个或多个由 INF 编写器定义的部分，这些部分用于在注册表中的现有 [REG_BINARY](/windows/desktop/SysInfo/registry-value-types)类型值项中设置或清除位。 但是，此指令很少用于设备/驱动程序 INF 文件中。
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
ms.openlocfilehash: b4c10fe83b19268af26ee85b05c4e02296ac0744
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820147"
---
# <a name="inf-bitreg-directive"></a>INF BitReg 指令


**注意**  如果要构建通用或移动驱动程序包，则此指令无效。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

**BitReg** 指令引用一个或多个由 INF 编写器定义的部分，这些部分用于在注册表中的现有 [REG_BINARY](/windows/desktop/SysInfo/registry-value-types)类型值项中设置或清除位。 但是，此指令很少用于设备/驱动程序 INF 文件中。

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


 
BitReg=bit-registry-section[,bit-registry-section]...
```

可以在上述正式语法语句中所示的任何节下指定 **BitReg** 指令。 还可以在以下任何一项由 INF 编写器定义的部分中指定此指令：

-   DDInstall 部分中的 [**AddService**](inf-addservice-directive.md)指令引用的 *服务安装部分* 或 *事件日志安装* 部分。
-   [**AddInterface**](inf-addinterface-directive.md)指令在 DDInstall 中引用的 *添加接口部分* [**_DDInstall_。接口**](inf-ddinstall-interfaces-section.md)部分。
-   [**InterfaceInstall32**](inf-interfaceinstall32-section.md)节中引用的 *安装界面部分*

**BitReg** 指令引用的每个命名部分都具有以下形式：

```inf
[bit-registry-section]
reg-root, [subkey], value-entry-name, [flags], byte-mask, byte-to-modify
reg-root, [subkey], value-entry-name, [flags], byte-mask, byte-to-modify
...
```

*位注册表部分* 可以有任意数量的条目，每个条目在单独的行中。

## <a name="entries"></a>项


<a href="" id="reg-root"></a>*注册表根*  
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
相对根−也就是说，使用此缩写指定的密钥相对于与 INF 部分关联的注册表项，其中显示此 **BitReg** 指令，如下表所示。

| 包含 BitReg 指令的 INF 部分                                    | HKR 引用的注册表项                                                        |
|----------------------------------------------------------------------------|---------------------------------------------------------------------------------------|
| INF [ * *_DDInstall_* _](inf-ddinstall-section.md)部分                   | 设备的 _software 密钥 * |
| INF [ * **DDInstall *。HW**](inf-ddinstall-hw-section.md)部分             | 设备的 *硬件密钥* |
| INF [ * **DDInstall *。Service**](inf-ddinstall-services-section.md)s 部分 | **服务** 密钥                                                                  |

 

**请注意**，**HKR** 不能用于从 INF [ * *_DefaultInstall_* _](inf-defaultinstall-section.md)部分引用的位注册表部分。  

 

有关存储在 _ *HKEY_LOCAL_MACHINE** 根下的驱动程序信息的详细信息，请参阅 [设备和驱动程序的注册表树和密钥](registry-trees-and-keys.md)。

<a href="" id="subkey"></a>*键值*  
此可选值可以表示为在 INF 的 [**字符串**](inf-strings-section.md)部分中定义的%*strkey*% 令牌，或在给定 *的* 注册表项下指定的注册表路径 (*key1 \\ key2 \\ key3*... ) ，指定包含要修改的值项的键。

<a href="" id="value-entry-name"></a>*值-输入名称*  
指定要修改的 (现有) 子项中现有 [REG_BINARY](/windows/desktop/SysInfo/registry-value-types)类型值条目的名称。 它可以表示为 "*带引号的字符串*" 或作为 INF 的 [**字符串**](inf-strings-section.md)部分中定义的%*strkey*% 令牌。

<a href="" id="flags"></a>*随意*  
此可选的十六进制值（以系统定义的低词和高位字标志值的运算位掩码表示）指定是否清除或设置给定字节掩码中指定的位。 其默认值为零，这会清除注册表的64位部分中的位。

其中每个标志的位掩码值如下所示：

<a href="" id="0x00000000--flg-bitreg-clearbits-"></a>**0x00000000** (FLG_BITREG_CLEARBITS)   
清除由 *字节掩码* 指定的位。

<a href="" id="0x00000001--flg-bitreg-setbits-"></a>**0x00000001** (FLG_BITREG_SETBITS)   
设置由 *字节掩码* 指定的位。

<a href="" id="0x00004000---flg-bitreg-32bitkey--"></a>**0x00004000** (FLG_BITREG_32BITKEY)    
 (Windows XP 和更高版本的 Windows。 ) 在32位注册表中进行指定的更改。 如果未指定，则对本机注册表进行更改。

<a href="" id="byte-mask"></a>*字节掩码*  
此以十六进制表示法表示的字节大小掩码指定要在给定的 *值输入名称* 的当前值中清除或设置的位。

<a href="" id="byte-to-modify"></a>*字节到修改*  
此以十进制表示的字节大小值指定要修改的 [REG_BINARY](/windows/desktop/SysInfo/registry-value-types)类型值中的字节的从零开始的索引。

<a name="remarks"></a>备注
-------

对于 INF 文件，每个 *注册表项节* 名称必须是唯一的，但它可以在同一 INF 的其他部分中由 **BitReg** 指令引用。 在 INF 文件中，每个 INF 编写器创建的节名称必须唯一，并且必须遵循用于定义节名称的常规规则。 有关这些规则的详细信息，请参阅 [INF 文件的一般语法规则](general-syntax-rules-for-inf-files.md)。

还可以修改现有 [REG_BINARY](/windows/desktop/SysInfo/registry-value-types)类型值项的值，方法是在 INF 文件中其他位置的 "添加注册表" 部分覆盖其当前值。 有关 "添加注册表" 部分的详细信息，请参阅 [**AddReg**](inf-addreg-directive.md)指令的参考。

使用 **BitReg** 指令需要定义另一个 INF 文件部分。 但是，在这种情况下，现有 [REG_BINARY](/windows/desktop/SysInfo/registry-value-types)类型值条目的值可以按位修改，从而保留所有剩余位的值。

<a name="examples"></a>示例
--------

下面的示例演示了一个用于虚拟应用程序的位注册表部分。

```inf
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

## <a name="see-also"></a>请参阅


[**AddInterface**](inf-addinterface-directive.md)

[**AddReg**](inf-addreg-directive.md)

[**AddService**](inf-addservice-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[**_DDInstall_* _](inf-ddinstall-section.md)

[_ *_DDInstall_。CoInstallers**](inf-ddinstall-coinstallers-section.md)

[**_DDInstall_。HW**](inf-ddinstall-hw-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

 

