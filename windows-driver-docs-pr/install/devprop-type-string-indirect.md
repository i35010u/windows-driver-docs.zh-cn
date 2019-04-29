---
title: DEVPROP_TYPE_STRING_INDIRECT
description: DEVPROP_TYPE_STRING_INDIRECT 标识符表示包含间接字符串引用的以 NULL 结尾的 Unicode 字符串的基本数据类型标识符。
ms.assetid: c3a4f627-02d7-47ba-aa62-5d6b0e8dd9cd
keywords:
- DEVPROP_TYPE_STRING_INDIRECT 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_STRING_INDIRECT
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7ab34cc95fffd5793b7cb93e5ea1584a9827dccf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391705"
---
# <a name="devproptypestringindirect"></a>DEVPROP_TYPE_STRING_INDIRECT


DEVPROP_TYPE_STRING_INDIRECT 标识符表示包含间接字符串引用的以 NULL 结尾的 Unicode 字符串的基本数据类型标识符。

<a name="remarks"></a>备注
-------

间接字符串引用描述包含实际的字符串的字符串资源。 间接字符串引用可以出现在以下格式之一：

<a href="" id="--path--filename--resourceid"></a>**@**\[<em>path</em>**\\**\]<em>FileName</em>**,-***ResourceID*  
Windows 从指定的模块中提取字符串*路径*并*FileName*条目和字符串的资源标识符由提供*ResourceID*条目 （不包括所需的负号）。 从最适合与调用方的首选的 UI 语言之一相匹配的模块资源部分加载字符串资源。 *路径*项是可选的。 如果指定*路径*条目，该模块必须位于系统定义的搜索路径中的目录。

<a href="" id="-infname--strkey-"></a>**@**<em>InfName</em>**，%**<em>strkey</em>**%**  
Windows 将从 INF 提取字符串**字符串**INF 文件在 %systemroot%部分\\*inf* directory 通过提供其名称*InfName*项。 *Strkey*令牌标识符应与中的行的键匹配**字符串**部分与一个调用方的最匹配的首选的 UI 语言。 如果没有特定于语言的**字符串**部分存在，则 Windows 将使用默认**字符串**部分。

您不能与属性数据类型修饰符的任何组合 DEVPROP_TYPE_STRING_INDIRECT。

### <a name="setting-a-property-of-this-type"></a>设置此类型的属性

若要设置其基本数据类型为 DEVPROP_TYPE_STRING_INDIRECT 的属性，调用对应 **SetupDiSet * * * Xxx*属性函数和集函数的输入参数，如下所示：

-   设置*PropertyType* DEVPROP_TYPE_STRING_INDIRECT 参数。

-   设置*PropertyBuffer*参数指向包含提供程序间接字符串引用的以 NULL 结尾的字符串的缓冲区的指针。

-   设置*PropertyBufferSize*的大小，以字节为单位的字符串的参数。

-   根据需要设置剩余函数参数设置的属性。

### <a name="retrieving-the-value-of-this-property-type"></a>检索此属性类型的值

当应用程序调用 **SetupDiGet * * * Xxx*属性函数来检索此基数据的属性的值类型，Windows 将尝试查找实际的属性引用的字符串。 如果 Windows 可以检索实际的字符串，它将实际字符串返回给调用方，并标识为检索到的属性的基本数据类型[ **DEVPROP_TYPE_STRING**](devprop-type-string.md)。 否则为 Windows 返回间接字符串引用，标识作为 DEVPROP_TYPE_STRING_INDIRECT 检索到的属性的基本数据类型。

### <a name="localizing-static-text"></a>本地化的静态文本

启动 Windows Vista 后，可以对自定义和标准的字符串类型即插即用静态文本属性，通过将静态文本属性类型设置为 DEVPROP_TYPE_STRING_INDIRECT 使用 PE 映像的字符串或资源表中的资源进行本地化。 此外可以添加可为静态文本格式设置的非本地化的替换字符串数据。

PE 映像的 STRINGTABLE 资源 （通常由 LoadString 执行） 中的字符串应使用以下格式：

"@"System32\\mydll.dll,-21\[;Fallback" String\]"

"@System32\\mydll.dll，-21\[;与 %1，%2 的回退字符串... 到 %n\[; (Arg1、 Arg2，...，ArgN)\]\]"

PE 映像的消息表资源 （通常由 RtlFindMessage，通常用在驱动程序的详细信息） 中的字符串应使用以下格式：

"@System32\\驱动程序\\mydriver.sys，\#21\[;回退字符串\]"

"@System32\\驱动程序\\mydriver.sys，\#21\[;与 %1，%2 的回退字符串... 到 %n\[; (Arg1、 Arg2，...，ArgN)\]\]"

"回退 String"是可选的但很有用，因为它可以返回如果资源无法找到或无法加载。 回退字符串也会返回的不模拟用户，并且这种情况下不能本地化的文本向用户显示仍的非交互式系统进程。

此技术，可对静态文本源自与调用方的区域设置最匹配的字符串或消息表资源进行本地化。

Windows 将格式化为字符串 （或回退字符串） 的尾随参数时它们从表中检索相应资源，更是如下所示相同的方式 RtlFormatMessage 一样。

自定义和标准的字符串类型即插即用静态文本进行本地化时加载资源从组件执行设置操作中，这通常发生在系统级别的组件的系统默认区域设置下设置的属性。

注意：PE 映像可以使用任一资源表类型 （STRINGTABLE 资源或消息表资源）。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>Windows Vista 和更高版本的 Windows。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpropdef.h （包括 Devpropdef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**DEVPROP_TYPE_STRING**](devprop-type-string.md)

 

 






