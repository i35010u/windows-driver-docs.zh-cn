---
title: INF Strings 节
description: INF 文件必须至少具有一个字符串部分，才能定义该 INF 中其他地方指定的每个 strkey 标记。
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
ms.openlocfilehash: 9d8ae4fe2aecf6284e2fa493406d6ab1306b2ca7
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223109"
---
# <a name="inf-strings-section"></a>INF Strings 节


INF 文件必须至少具有一个**字符串**部分，才能定义该 inf 中其他地方指定的每个%*strkey*% 令牌。

```inf
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


<a href="" id="strkey1--strkey2-----"></a>*strkey1*， *strkey2*，.。。  
INF 文件中的每个字符串键都必须指定一个唯一的名称，该名称包含字母、数字和/或其他显式可见字符。 此类*strkey*标记中的% 字符必须表示为**%%**。

<a href="" id="some-string----some-string-"></a>*某些字符串* | **"**<em>some string</em>**"**  
指定一个字符串，可以选择性地用双引号（"）分隔，其中包含字母、数字、标点符号，甚至可能是某些隐式可见字符，特别是内部空间和/或制表符。 但是，未加引号的字符串不能包含内部双引号（"）、分号（;)、换行符、返回或任何不可见的控制字符，也不能包含反斜杠\) （作为其最终字符）。

<a href="" id="------string-with-leading-or-trailing-whitespace-----------"></a>**"* **     带前导或尾随空格的字符串*     **" * * |   

<a href="" id="-very-long-multiline-string----"></a>**"**<em>非常长的多行字符串</em>**"** |   

<a href="" id="-string-with-semicolon----"></a>**"**<em>带有分号的字符串</em>**"** |   

<a href="" id="-string-ending-in-backslash---"></a>**"**<em>字符串结尾-反斜杠</em>**"** |  

<a href="" id="--double-quoted-string-value--"></a>**""***带双引号的字符串-值 "***"**  
如果为%*strkey*% token 指定的值满足以下任一条件，则*必须*将该值用双引号（"）引起来：

-   如果指定的字符串具有必须保留为其值的一部分的前导空格或尾随空格，则必须用双引号将该字符串括起来，以防止 INF 分析器丢弃其前导空格和/或尾随空格。
-   如果长字符串可能包含任何内部换行或返回字符（因为文本编辑器中的换行），则它也应该用双引号引起来，以防止在初始内部换行或返回字符处截断字符串。
-   如果此类字符串包含分号，则必须将其括在双引号中，以防止在分号处截断字符串。 （正如[Inf 文件一般语法规则](general-syntax-rules-for-inf-files.md)中所述，分号字符在 inf 文件中开始每个注释。）
-   如果此类字符串以反斜杠结尾，则必须用双引号引起来，以防止字符串与下一项连接。 （正如 INF 文件一般语法规则中所述，反斜杠字符（\)用作 inf 文件中的 continuator 行）。
-   与不带引号的字符串规范一样，此类 "带引号的字符串" 不能包含内部双引号字符。 不过，可以使用一个或多个附加的双引号字符（例如，"" 部分字符串 ""）将其指定为用双引号引起来的字符串值。

    INF 分析器不仅会丢弃此部分中任何 "带引号的字符串" 的最外面的封闭双引号，还会会将每个后续的双引号对一个双引号字符。

    例如，在分析时，"" "某些字符串" "也会变成" 某些字符串 "。

总之，如果满足以下任一条件，则任何字符串都必须包含在一对双引号字符（"）中：

-   字符串包含前导空格或尾随空格。
-   如果此字符串已换行，则该字符串很长。
-   字符串包含分号或最后一个反斜杠字符。
-   字符串本身是一个带引号的字符串。

系统 INF 分析器会丢弃最外面的一对双引号字符，这些字符用于分隔此类字符串以及双引号字符串分隔符之外的任何前导或尾随空格字符。

<a name="remarks"></a>备注
-------

由于系统 inf 分析器从定义%*strkey*% 令牌的任何 **"**<em>带引号的字符串</em>**"** 中去除了最外面的封闭双引号，因此许多系统 inf 文件将所有%*strkey*% 令牌定义为 **"**<em>带引号的字符串</em><strong>"</strong>，以避免在 INF 分析期间意外丢失前导空格和尾随空格。 使用 **"**<em>带引号的字符串</em><strong>"</strong>还可以确保无法截断跨行换行的更长字符串值，并且无法将带有结束反斜杠的字符串连接到 INF 文件中的下一行。

若要创建单个国际 INF 文件，INF 可以具有一组特定于区域设置的**字符串。**<em>LanguageID</em>节，如正式语法语句中所示。 *LanguageID*扩展是一个十六进制值，定义如下：

-   较小的10位包含主要语言 ID，接下来的6位包含 "子语言 ID"，由*Winnt*中定义的 MAKELANGID 宏指定。
-   语言和子语言 Id 必须与 Winnt 中定义的 Win32 LANG_*xxx*和 SUBLANG_*XXX*常量的系统定义的值相匹配 *。*

例如， *LanguageID*的值为0x0407，表示主要语言 id LANG_GERMAN （07），其中的子语言 id 为 SUBLANG_GERMAN （01）。

INF 文件只能包含一个**字符串**和一个**字符串。** 每个*LanguageID*值的<em>LanguageID</em>部分。

Windows 选择一个**字符串**部分用于转换用于安装的所有%*strkey*% 令牌。 根据特定计算机的当前区域设置，Windows 会按以下方式选择**字符串**部分：

1.  Windows 首先查找 *。* INF 中与分配给计算机的当前区域设置相匹配的 LanguageID 值。 如果找到完全匹配项，Windows 将使用该**LanguageID** inf 部分来转换 INF 中定义的所有%*strkey*% 令牌。
2.  否则，Windows 会查找 "下一步"，以查找 LANG_*xxx*值的匹配项，并将 SUBLANG_NEUTRAL 的值作为 SUBLANG_*XXX*。 如果找到此匹配项，Windows 将使用该 INF 部分来转换 INF 中定义的所有%*strkey*% 令牌。
3.  否则，Windows 会查找 "下一步"，以匹配 LANG_*xxx*值和相同 LANG_*xxx*系列的任何有效 SUBLANG_*xxx* 。 如果找到这样的部分匹配项，请使用 LanguageID INF 部分来转换 INF 中定义的所有%*strkey*% 令牌。
4.  否则，Windows 会将未修饰的字符串部分用于在 INF 中定义的所有转换%*strkey*% 令牌。

按照约定，为国际市场创建一组 INF 文件，为方便起见，**字符串**部分是所有系统 INF 文件中的最后一个。 对于 INF 中所有用户可见的字符串值使用%*strkey*% 令牌，并将其放入每个区域设置**字符串**部分，简化了此类字符串的转换。 有关特定于区域设置的 INF 文件的详细信息，请参阅[创建国际 INF 文件](creating-international-inf-files.md)。

尽管**字符串**部分是每个 inf 文件中的最后一个部分，但在**字符串**部分中定义的任何指定的%*strkey*% 令牌都可以在 INF 中的其他位置重复使用（特别是在需要该令牌的翻译值需要时）。 [Setupapi.log](setupapi.md)函数将每个%*strkey*% 令牌展开为指定的字符串，然后使用该扩展值进行更多 INF 处理。

在 INF 文件中使用%*strkey*% 令牌并不限于用户可见的字符串值。 只要在**字符串**部分中定义了每个标记，就可以使用任何对 INF 编写器都方便的方式使用这些标记。 例如，当你编写需要多个 Guid 规范的 INF 文件时，通过使用有意义的名称作为每个此类 GUID 值的替代方法，可以方便地为每个 GUID 创建%*strkey*% 令牌。

在 INF 文件的**%****字符串**部分指定一组<em>strkey</em>**% = "{**<em>GUID</em>**}"** 值需要只键入每个显式 GUID 值一次。 与在整个 INF 文件中使用显式 GUID 值相比，这可以提供更具可读性的内部 INF 文档。

所有%*strkey*% 令牌必须在引用它们的 INF 文件中定义。 因此，对于具有 "**包含**" 和 "**需要**" 条目的任何 inf 文件，包含的 inf 都必须有其自己的**字符串**部分，才能定义该 inf 中引用的所有%*strkey*% 令牌。

在 INF**字符串**部分，包含终止 NULL 字符的替换字符串的最大长度（以字符为4096）为（windows Vista 和更高版本的 windows）和512（windows Server 2003、windows XP 和 windows 2000）。 字符串替换后，INF 文件字符串的最大长度（以字符为4096）为，包括终止 NULL 字符。

<a name="examples"></a>示例
--------

下面的示例演示了一个来自系统提供的特定于区域设置的本地*dvd*的**字符串**部分片段，适用于英语的国家/地区。

```inf
[Strings]
Msft="Microsoft"
MfgToshiba="Toshiba"
Tosh404.DeviceDesc="Toshiba DVD decoder card"
; ... 
```

下面的示例演示字符串串联。

```inf
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

## <a name="see-also"></a>另请参阅


[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall*.CoInstallers**](inf-ddinstall-coinstallers-section.md)

[***DDInstall*.HW**](inf-ddinstall-hw-section.md)

[***DDInstall*.接口**](inf-ddinstall-interfaces-section.md)

[***DDInstall*.服务器**](inf-ddinstall-services-section.md)

[**制造商**](inf-manufacturer-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[***模型***](inf-models-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**版本**](inf-version-section.md)

 

 






