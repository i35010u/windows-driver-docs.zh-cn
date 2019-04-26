---
title: INF Ini2Reg 指令
description: Ini2Reg 指令引用一个或多个命名的部分中的行或从提供的 INI 文件的部分将移动到注册表。 这将创建或替换指定键下的一个或多个值项。
ms.assetid: 82c7ffb5-7e49-4256-b10a-d7be5df2336a
keywords:
- INF Ini2Reg 指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF Ini2Reg Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7bb47ba37497f378082b855452ab8db79f334df3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330256"
---
# <a name="inf-ini2reg-directive"></a>INF Ini2Reg 指令


**请注意**  如果要构建一个通用或移动设备的驱动程序包，此指令无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

**Ini2Reg**指令引用一个或多个命名的部分中的行或从提供的 INI 文件的部分将移动到注册表。 这将创建或替换指定键下的一个或多个值项。

```ini
        [
        DDInstall
        ] | 
[DDInstall.CoInstallers] | 
[ClassInstall32] | 
[ClassInstall32.ntx86] | 
[ClassInstall32.ntia64] |  (Windows XP and later versions of Windows)
[ClassInstall32.ntamd64]  (Windows XP and later versions of Windows)
[ClassInstall32.ntarm]  (Windows 8 and later versions of Windows)
[ClassInstall32.ntarm64]  (Windows 10 and later versions of Windows)


  
Ini2Reg=ini-to-registry-section[,ini-to-registry-section]...
```

每个命名部分引用的**Ini2Reg**指令具有以下形式：

```ini
[ini-to-registry-section]
 
ini-file,ini-section,[ini-key],reg-root,subkey[,flags]
...
```

*注册表部分 ini*可以具有任意 INF 编写器确定数量的条目，每个单独的行上。

## <a name="entries"></a>条目


<a href="" id="ini-file"></a>*ini-file*  
指定的源媒体上提供的 INI 文件的名称。 此值可以表示为*文件名*或作为 %*strkey*中定义的 %令牌[**字符串**](inf-strings-section.md) INF 文件部分。

<a href="" id="ini-section"></a>*ini-section*  
指定包含要复制的注册表信息的给定 INI 文件中的部分的名称。

<a href="" id="ini-key"></a>*ini-key*  
在要复制到注册表的 INI 文件中指定的密钥的名称。 如果省略此值，则整个*ini 部分*是要传输到指定的注册表*子项*。

<a href="" id="reg-root"></a>*reg-root*  
标识在此条目中提供的其他值的注册表树的根。 有关详细信息，请参阅参考[ **AddReg 指令**](inf-addreg-directive.md)。

<a href="" id="subkey"></a>*subkey*  
标识要接收的值的子项表示为 %*strkey*中定义的 %令牌[**字符串**](inf-strings-section.md)部分的 INF 或显式的注册表路径 (<em>key1</em>**\\**<em>key2</em>**\\**<em>key3</em>...) 从给定*reg 根*。

<a href="" id="flags"></a>*flags*  
指定如何处理转移之后的给定的信息对注册表和/或 （以位 1） 是否覆盖现有的注册表信息，如下所示的 INI 文件 （以位 0）：

<a href="" id="bit-zero---0"></a>Bit 0 = **0**  
给定的信息从删除 INI 文件后将其复制到注册表。 这是默认设置。

<a href="" id="bit-zero---1"></a>Bit 0 = **1**  
将其移到注册表后从 INI 文件中删除给定的信息。

<a href="" id="bit-one---0"></a>一个位 = **0**  
如果在注册表中已存在指定的子项，不会传输 INI 提供信息到此*子项*。 否则，创建指定*子项*作为其值项此 INI 提供的信息与注册表中。 这是默认设置。

<a href="" id="bit-one---1"></a>一个位 = **1**  
如果在注册表中已存在指定的子项，其值条目将替换为 INI 提供信息。

<a name="remarks"></a>备注
-------

**Ini2Reg**指令在任何正式语法语句中所示的部分是否有效。 此指令也是有效引用的 INF 编写器定义各节中[ **AddInterface** ](inf-addinterface-directive.md)指令或在引用[ **InterfaceInstall32**](inf-interfaceinstall32-section.md)部分。

如果一个 INF 文件用于在 Windows XP 和更高版本的 Windows 上安装的设备，不应包含的 INF 文件**Ini2Reg**指令。 INF 文件，其中包含**Ini2Reg**指令不会传递["设计 Windows"徽标测试](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver)，将不会收到数字签名，并因此将信任的 Windows (请参阅[如何Windows 中选择驱动程序](how-setup-selects-drivers.md))。

每个*注册表部分 ini*名称必须是唯一的 INF 文件。 每个 INF 编写器创建的部分名称的 INF 文件中必须是唯一和必须遵从常规规则，用于定义的节名称。 有关这些规则的详细信息，请参阅[INF 文件的常规语法规则](general-syntax-rules-for-inf-files.md)。

INF 提供的完整路径给定*ini 文件*中通过以下方式之一在分发媒体：

-   在提供 IHV/OEM INF 文件中，通过使用[ **SourceDisksNames** ](inf-sourcedisksnames-section.md) ，并且可能[ **SourceDisksFiles** ](inf-sourcedisksfiles-section.md)到此 INF 部分显式指定在分发媒体的根目录 （或目录） 中不是每个命名的源文件的完整路径。
-   在系统提供 INF 文件中，通过提供一个或多个附加 INF 文件中标识**LayoutFile**中的条目[**版本**](inf-version-section.md) INF 文件部分。

## <a name="see-also"></a>请参阅


[**AddInterface**](inf-addinterface-directive.md)

[**AddReg**](inf-addreg-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall*.CoInstallers**](inf-ddinstall-coinstallers-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**Strings**](inf-strings-section.md)

[**UpdateIniFields**](inf-updateinifields-directive.md)

[**UpdateInis**](inf-updateinis-directive.md)

[**版本**](inf-version-section.md)

 

 






