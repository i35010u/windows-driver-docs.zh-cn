---
title: INF Strings 节
description: INF 文件必须具有至少一个字符串部分来定义该 INF 中指定其他位置的每个 strkey 标记。
ms.assetid: 7352aa82-a7cd-4d15-9a9e-e03985f6006e
keywords:
- INF 字符串部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF Strings Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d69c976faa7309f56d2b16344fd3d41c46ccb619
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325799"
---
# <a name="inf-strings-section"></a>INF Strings 节


INF 文件必须至少一个**字符串**部分来定义每 %*strkey*%令牌在该 INF 中指定其他位置。

```ini
[Strings] | 
[Strings.LanguageID] ...
 
strkey1 = ["]some string["]
strkey2 = "    string-with-leading-or-trailing-whitespace     "  | 
          "very-long-multiline-string" | 
          "string-with-semicolon" | 
          "string-ending-in-backslash" |
          ""double-quoted-string-value""
 ...
```

## <a name="entries"></a>条目


<a href="" id="strkey1--strkey2-----"></a>*strkey1*, *strkey2*, ...  
INF 文件中的每个字符串密钥必须指定包含字母、 数字，和/或其他显式可见的字符的唯一名称。 此类中的 %字符*strkey*令牌必须表示为 **%%** 。

<a href="" id="some-string----some-string-"></a>*某些字符串* |  **"** <em>一些字符串</em> **"**  
指定的字符串，可以选择使用两个双引号字符 （"），包含字母、 数字、 标点符号和甚至某些隐式可见的字符，具体而言，内部的空间和/或制表符分隔。 但是，不带引号的字符串不能包含内部双引号引起来 （'）、 分号 （;）、 换行符、 返回时或任何不可见控件字符，而且不能包含反斜杠 (\)作为其最后一个字符。

<a href="" id="------string-with-leading-or-trailing-whitespace-----------"></a> **"** *     string-with-leading-or-trailing-whitespace*     **"** |   

<a href="" id="-very-long-multiline-string----"></a> **"** <em>very-long-multiline-string</em> **"**  |   

<a href="" id="-string-with-semicolon----"></a> **"** <em>string-with-semicolon</em> **"**  |   

<a href="" id="-string-ending-in-backslash---"></a> **"** <em>string-ending-in-backslash</em> **"**  |  

<a href="" id="--double-quoted-string-value--"></a> **"***"double-quoted-string-value"***"**  
%为指定的值*strkey*%令牌*必须*括在双引号 （"） 中，如果它满足以下条件的任何：

-   如果指定的字符串具有前导或尾随空格，必须保留其值的一部分，该字符串必须括在双引号字符以防止其前导和/或尾随空格被放弃 INF 分析器中。
-   如果一个长字符串可能包含任何内部换行符或回车符，由于在文本编辑器中换行，应也括在双引号内以防止发生截断在初始内部换行字符串或返回字符。
-   如果此类字符串包含分号，它必须括在双引号内以避免字符串分号处被截断。 (如前面所述[INF 文件的常规语法规则](general-syntax-rules-for-inf-files.md)，分号字符开始 INF 文件中的每个注释。)
-   如果此类字符串以反斜杠结尾，它必须括在双引号内以防止与下一个条目被串联字符串中。 (如前所述已在一般情况下语法规则的 INF 文件，反斜杠字符 (\)用作行 continuator INF 文件中。)
-   不带引号的字符串规范等此类"带引号的字符串"不能包含内部双引号字符。 但是，它可以将指定为显式双引号分隔的字符串值使用一个或多个其他两个双引号字符 （例如，""一些字符串""） 对。

    INF 分析器不仅将放弃最外面的封闭双引号引起来的任何"带引号的字符串"在此部分中，对，而且还会双引号将每个后续顺序对将转换为单个双引号字符。

    例如，"""一些字符串"""也将变为"一些字符串"时进行分析。

总之，任何字符串必须括在一对双引号字符 （"） 如果任意下列条件成立：

-   此字符串包含前导或尾随空格。
-   该字符串是使长时间，其行包装。
-   该字符串包含分号或最终反斜杠字符。
-   该字符串本身是带引号的字符串。

系统 INF 分析器将丢弃 double 引号字符来分隔此类字符串，以及带有在两个双引号字符串分隔符外任何前导或尾随空白字符的最外面的封闭对。

<a name="remarks"></a>备注
-------

由于系统 INF 分析器会剥离最外面的封闭从任何两个双引号对因此 **"** <em>带引号的字符串</em> **"** 定义 %*strkey*%令牌，许多系统 INF 文件定义所有 %*strkey*%令牌作为 **"** <em>带引号的字符串</em><strong>"</strong>秒以避免前导空格和尾随空格 INF 分析期间的意外的丢失。 利用 **"** <em>带引号的字符串</em><strong>"</strong>s 还确保该特别长字符串包装在行之间的值不能被截断，并且该字符串末尾有反斜杠无法连接到 INF 文件中的下一行。

若要创建一个国际 INF 文件，INF 可以具有一组特定于区域设置**字符串。** <em>LanguageID</em>节，如正式语法语句中所示。 *LanguageID*扩展是一个十六进制值，如下所示定义：

-   较低的 10 位包含主语言 ID，接下来的 6 位包含子语言 ID，如果指定由中定义的 MAKELANGID 宏*Winnt.h*。
-   语言和子语言 Id 必须匹配系统定义的值的 Win32 LANG_*XXX*和 SUBLANG_*XXX*中定义的常量*Winnt.h 中的。*

例如， *LanguageID* 0x0407 值表示主语言 ID LANG_GERMAN (07) 与子语言 ID SUBLANG_GERMAN (01)。

INF 文件只能包含一个**字符串**部分中的，以及一个**字符串。** <em>LanguageID</em>部分，了解每个*LanguageID*值。

Windows 选择单个**字符串**节，用来转换所有 %*strkey*%令牌进行安装。 具体取决于特定计算机的当前区域设置，选择 Windows**字符串**部分如下所示：

1.  Windows 将首先查找 *。LanguageID* INF 匹配分配给计算机的当前区域设置的值。 如果找到完全匹配，Windows 将使用该**Strings.LanguageID** INF 部分转换所有 %*strkey*INF 中定义的 %令牌。
2.  否则，Windows 中查找下一个匹配项到 LANG_*XXX*值与的值作为 SUBLANG_ SUBLANG_NEUTRAL*XXX*。 如果找到这样的匹配，则 Windows 将使用该 INF 部分将所有 %*strkey*INF 中定义的 %令牌。
3.  否则，Windows 中查找下一个匹配项到 LANG_*XXX*值和任何有效 SUBLANG_*XXX*的同一个 LANG_*XXX*系列。 如果找到此类的部分匹配，则使用该 Strings.LanguageID INF 部分转换所有 %*strkey*INF 中定义的 %令牌。
4.  否则，Windows 使用的未修饰的字符串部分对所有转换 %*strkey*INF 中定义的 %令牌。

按照约定，并为方便起见，在创建一组针对国际市场的 INF 文件**字符串**部分介绍了所有系统 INF 文件中的最后一个。 使用 %*strkey*%中 INF 中，并将其置于每个区域设置中的所有用户可见的字符串值的令牌**字符串**部分中，简化了此类字符串的翻译。 有关特定于区域设置的 INF 文件的详细信息，请参阅[创建国际 INF 文件](creating-international-inf-files.md)。

尽管**字符串**部分中的每个 INF 文件的最后一个部分，任何指定的 %*strkey*中定义的 %令牌**字符串**中可以重复其他位置使用部分INF，特别是，无论此标记的已转换的值是必需的。 [SetupAPI](setupapi.md)函数展开每个 %*strkey*到指定的字符串，然后使用扩展值来进行进一步 INF 处理 %令牌。

使用 %*strkey*INF 文件内的 %令牌并不局限于用户可见的字符串值。 只要中定义的每个标记，可以方便 INF 编写器，以任何方式使用这些令牌**字符串**部分。 例如，当您编写需要多个 Guid 指定的 INF 文件，可能会方便地创建 %*strkey*%令牌为每个 GUID，通过为每个此类的 GUID 值的替代使用有意义的名称。

指定一组 **%** <em>strkey</em> **%="{** <em>GUID</em> **}"** INF 文件中的值**字符串**部分要求仅一次键入每个显式的 GUID 值。 这可以帮助提供更具可读性内部的 INF 文件比通过在整个 INF 文件中使用显式的 GUID 值。

所有 %*strkey*%令牌必须引用这些 INF 文件内定义。 因此，对于具有任何 INF 文件**Include**并**需要**项，包括 INF 必须具有其自己**字符串**部分，以定义所有 %*strkey*该 INF 中引用的 %令牌。

在 INF**字符串**部分中，以字符为单位的替换字符串，包括终止 NULL 字符，最大长度为 4096 （Windows Vista 和更高版本的 Windows） 和 512 (Windows Server 2003、 Windows XP、 和Windows 2000)。 字符串替换后以字符为单位的 INF 文件字符串的最大长度为 4096，包括终止 NULL 字符。

<a name="examples"></a>示例
--------

下面的示例演示的一个片段**字符串**从系统提供区域设置特定的部分*dvd.inf*说英语的国家/地区中安装的。

```ini
[Strings]
Msft="Microsoft"
MfgToshiba="Toshiba"
Tosh404.DeviceDesc="Toshiba DVD decoder card"
; ... 
```

下面的示例演示字符串串联。

```ini
[OEM Windows System Component Verification]
OID = 1.3.6.1.4.1.311.10.3.7    ; WHQL OEM OID 
Notice = "%A% %B% %C% %D% %E%" 
[Strings]
A = "This certificate is used to sign untested drivers that have not passed the Windows Hardware Quality Labs (WHQL) testing process."
B = "This certificate and drivers signed with this certificate are intended for use in test environments only, and are not intended for use in any other context."
C = "Vendors who distribute this certificate or drivers signed with this certificate outside a test environment may be in violation of their driver signing agreement."
D = "Vendors who have their drivers signed with this certificate do so at their own risk." 
E = "In particular, Microsoft assumes no liability for any damages that may result from the distribution of this certificate or drivers signed with this certificate outside the test environment described in a vendor's driver signing agreement."
```

## <a name="see-also"></a>请参阅


[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall*.CoInstallers**](inf-ddinstall-coinstallers-section.md)

[***DDInstall *。硬件**](inf-ddinstall-hw-section.md)

[***DDInstall *。接口**](inf-ddinstall-interfaces-section.md)

[***DDInstall*.Services**](inf-ddinstall-services-section.md)

[**制造商**](inf-manufacturer-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[***模型***](inf-models-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**版本**](inf-version-section.md)

 

 






