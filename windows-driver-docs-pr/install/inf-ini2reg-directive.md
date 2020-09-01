---
title: INF Ini2Reg 指令
description: Ini2Reg 指令引用一个或多个已命名的节，其中所提供的 INI 文件中的行或节被移到注册表中。 这会创建或替换指定键下的一个或多个值项。
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
ms.openlocfilehash: 0b0c56b7ee9a8075002eb933fadc75f9899564ea
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097307"
---
# <a name="inf-ini2reg-directive"></a>INF Ini2Reg 指令


**注意**   如果要构建通用或移动驱动程序包，则此指令无效。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

**Ini2Reg**指令引用一个或多个已命名的节，其中所提供的 INI 文件中的行或节被移到注册表中。 这会创建或替换指定键下的一个或多个值项。

```inf
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

**Ini2Reg**指令引用的每个命名部分都具有以下形式：

```inf
[ini-to-registry-section]
 
ini-file,ini-section,[ini-key],reg-root,subkey[,flags]
...
```

*Ini 到注册表部分*可以有任何由 INF 编写器决定的条目数，每个条目在单独的行中。

## <a name="entries"></a>项


<a href="" id="ini-file"></a>*ini-文件*  
指定在源媒体上提供的 INI 文件的名称。 此值可以表示为*文件名*，也可以表示为在 INF 文件的[**字符串**](inf-strings-section.md)部分中定义的%*strkey*% 令牌。

<a href="" id="ini-section"></a>*ini-部分*  
指定指定 INI 文件中包含要复制的注册表信息的部分的名称。

<a href="" id="ini-key"></a>*ini-密钥*  
指定 INI 文件中要复制到注册表的密钥的名称。 如果省略此值，则会将整个 *ini 部分* 传输到指定的注册表 *子项*。

<a href="" id="reg-root"></a>*注册表根*  
标识此项中提供的其他值的注册表树的根。 有关详细信息，请参阅 [**AddReg 指令**](inf-addreg-directive.md)的参考。

<a href="" id="subkey"></a>*键值*  
标识用于接收值的子项，该子项表示为在 INF 的[**字符串**](inf-strings-section.md)部分中定义的%*strkey*% 令牌，或从给定的注册表项的 ) 的显式注册表路径 (<em>key1</em> **\\** <em>key2</em> **\\** <em>key3</em>... *reg-root*。

<a href="" id="flags"></a>*随意*  
指定在位 0) 如何处理 INI 文件的 (，在将给定的信息传输到注册表和/或 (时，) 是否覆盖现有注册表信息，如下所示：

<a href="" id="bit-zero---0"></a>位 0 = **0**  
将给定信息复制到注册表后，不要将其从 INI 文件中删除。 这是默认值。

<a href="" id="bit-zero---1"></a>位 0 = **1**  
将给定信息移入注册表后，从 INI 文件中删除该信息。

<a href="" id="bit-one---0"></a>位 one = **0**  
如果注册表中已经存在指定的子项，请不要将 INI 提供的信息传输到该 *子项*。 否则，请在注册表中创建指定的 *子项* ，并将此 INI 提供的信息作为其值输入。 这是默认值。

<a href="" id="bit-one---1"></a>位 one = **1**  
如果注册表中已存在指定的子项，请将其值项替换为 INI 提供的信息。

<a name="remarks"></a>备注
-------

**Ini2Reg**指令在正式语法语句中显示的任何节中都有效。 此指令在 INF-由 [**AddInterface**](inf-addinterface-directive.md) 指令引用或在 [**InterfaceInstall32**](inf-interfaceinstall32-section.md) 节中引用的由编写者定义的部分中有效。

如果使用 INF 文件在 Windows XP 和更高版本的 Windows 上安装设备，则 INF 文件不应包含 **Ini2Reg** 指令。 包含 **Ini2Reg** 指令的 INF 文件将不会传递 ["设计用于 Windows" 徽标测试](/windows-hardware/drivers)，不会收到数字签名，因此将不受 Windows (查看 [windows 如何选择驱动程序](how-setup-selects-drivers.md)) 。

对于 INF 文件，每个 *ini 到注册表分区* 名称必须是唯一的。 在 INF 文件中，每个 INF 编写器创建的节名称必须唯一，并且必须遵循用于定义节名称的常规规则。 有关这些规则的详细信息，请参阅 [INF 文件的一般语法规则](general-syntax-rules-for-inf-files.md)。

INF 通过以下方式之一在分发介质上提供给定 *ini 文件* 的完整路径：

-   在 IHV/OEM 提供的 INF 文件中，使用 [**SourceDisksNames**](inf-sourcedisksnames-section.md) 和（可能为）的 [**SourceDisksFiles**](inf-sourcedisksfiles-section.md) 部分显式指定每个命名源文件的完整路径，该文件不在根目录中 (或) 在分发媒体上。
-   在系统提供的 INF 文件中，通过提供一个或多个其他 INF 文件，在 INF 文件的[**版本**](inf-version-section.md)部分的**LayoutFile**项中标识。

## <a name="see-also"></a>另请参阅


[**AddInterface**](inf-addinterface-directive.md)

[**AddReg**](inf-addreg-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall*.CoInstallers**](inf-ddinstall-coinstallers-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**字符串**](inf-strings-section.md)

[**UpdateIniFields**](inf-updateinifields-directive.md)

[**UpdateInis**](inf-updateinis-directive.md)

[**版本**](inf-version-section.md)

 

