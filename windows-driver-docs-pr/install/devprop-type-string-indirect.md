---
title: DEVPROP_TYPE_STRING_INDIRECT
description: DEVPROP_TYPE_STRING_INDIRECT 标识符表示以 NULL 结尾的 Unicode 字符串的基本数据类型标识符，其中包含间接字符串引用。
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
ms.openlocfilehash: 758dc0fa47abafaf0c9ce5e8a48b31aa56bece46
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791473"
---
# <a name="devprop_type_string_indirect"></a>DEVPROP_TYPE_STRING_INDIRECT


DEVPROP_TYPE_STRING_INDIRECT 标识符表示以 NULL 结尾的 Unicode 字符串的基本数据类型标识符，其中包含间接字符串引用。

<a name="remarks"></a>备注
-------

间接字符串引用描述了包含实际字符串的字符串资源。 间接字符串引用可能以下列格式之一出现：

<a href="" id="--path--filename--resourceid"></a>**@**\[<em>path</em> **\\** 路径 \]<em>FileName</em>**，-**_ResourceID_  
Windows 从 *路径* 和 *文件名* 条目指定的模块中提取字符串，并且该字符串的资源标识符由 *ResourceID* 条目提供 (不包括必需的减号) 。 从与调用方的首选 UI 语言之一最匹配的模块资源部分加载字符串资源。 *路径* 条目是可选的。 如果指定 *路径* 条目，则该模块必须位于系统定义的搜索路径中的目录中。

<a href="" id="-infname--strkey-"></a>**@**<em>InfName</em>**、%**<em>strkey</em>**%**  
Windows 从% SystemRoot% **Strings** \\ *INF* 目录（其名称由 *InfName* 项提供）中 inf 文件的 inf 字符串部分提取字符串。 *Strkey* 标记标识符应与 **字符串** 部分中的行的键匹配，这与调用方的首选 UI 语言之一匹配。 如果不存在特定于语言的 **字符串** 部分，则 Windows 将使用默认 **字符串** 部分。

不能将 DEVPROP_TYPE_STRING_INDIRECT 与任何属性数据类型修饰符组合在一起。

### <a name="setting-a-property-of-this-type"></a>设置此类型的属性

若要设置其基本数据类型为 DEVPROP_TYPE_STRING_INDIRECT 的属性，请调用相应的 **SetupDiSet**_Xxx_ 属性函数并按如下所示设置函数输入参数：

-   将 *PropertyType* 参数设置为 DEVPROP_TYPE_STRING_INDIRECT。

-   将 *PropertyBuffer* 参数设置为指向包含以 NULL 结尾的字符串（提供间接字符串引用）的缓冲区的指针。

-   将 *PropertyBufferSize* 参数设置为字符串的大小（以字节为单位）。

-   根据需要设置其余函数参数来设置属性。

### <a name="retrieving-the-value-of-this-property-type"></a>检索此属性类型的值

当应用程序调用 **SetupDiGet**_Xxx_ 属性函数检索此基本数据类型的属性值时，Windows 将尝试查找该属性引用的实际字符串。 如果 Windows 可以检索实际的字符串，它会将实际字符串返回给调用方，并将检索到的属性的基本数据类型标识为 [**DEVPROP_TYPE_STRING**](devprop-type-string.md)。 否则，Windows 将返回间接字符串引用，并将检索到的属性的基本数据类型标识 DEVPROP_TYPE_STRING_INDIRECT。

### <a name="localizing-static-text"></a>本地化静态文本

从 Windows Vista 开始，可以通过将静态文本属性类型设置为 DEVPROP_TYPE_STRING_INDIRECT，使用 PE 映像的字符串或资源表中的资源来本地化自定义和标准字符串类型 PnP 静态文本属性。 还可以添加可格式化为静态文本的非本地化的替换字符串数据。

位于 PE 映像的 STRINGTABLE 资源中的字符串 (通常由 LoadString) 执行，则应使用以下格式：

"@" System32 \\mydll.dll，-21 \[ ;回退 "String \] "

" @System32 \\mydll.dll、-21 \[ ;回退字符串与 %1、%2 .。。 到% n \[ ; (Arg1，Arg2,..., ArgN) \] \] "

位于 PE 映像的消息表资源中的字符串 (通常由 RtlFindMessage 执行，更常用于驱动程序) 应使用以下格式：

" @System32 \\ 驱动程序 \\mydriver.sys， \# 21 \[ ;回退字符串 \] "

" @System32 \\ 驱动程序 \\mydriver.sys， \# 21 \[ ;回退字符串与 %1、%2 .。。 到% n \[ ; (Arg1，Arg2,..., ArgN) \] \] "

"回退字符串" 是可选的，但很有用，因为如果找不到或无法加载资源，则可以将其返回。 回退字符串还会返回到未模拟用户的非交互式系统进程，因此不能将本地化的文本显示给用户。

利用此方法，您可以从与调用方的区域设置最匹配的字符串或消息表资源中对拉取的静态文本进行本地化。

在从相应的资源表检索后，Windows 会将尾随参数的格式设置为字符串 (或回退字符串) ，这与 RtlFormatMessage 的方式大致相同。

自定义和标准字符串类型 PnP 静态文本在你通过从执行集操作的组件中加载资源来进行本地化，此操作通常发生在系统级组件的系统默认区域设置下。

注意： PE 映像可以使用资源表类型 (STRINGTABLE 资源或) 消息表资源。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>Windows Vista 和更高版本的 Windows。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Devpropdef (包含 Devpropdef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**DEVPROP_TYPE_STRING**](devprop-type-string.md)

 

 






