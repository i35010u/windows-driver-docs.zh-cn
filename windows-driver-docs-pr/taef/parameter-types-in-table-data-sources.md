---
title: 表数据源中的参数类型
description: 表数据源中的参数类型
ms.assetid: 034F171E-716F-4795-9B07-46A109052227
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3004599456191567616a82ae54546f5ac447f59
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521219"
---
# <a name="parameter-types-in-table-data-sources"></a>表数据源中的参数类型


下表的提供摘要表中可用的各种参数类型的基于数据源和字符串的类型可用于使数据源文件兼容在纯模式、 管理和编写脚本的测试。

本机管理脚本 ParameterType LanguageType ParameterType LanguageType ParameterType LanguageType"String"WEX::Common::String"String"字符串"String"或"BSTR"VT\_BSTR"int"int"Int32"或"int"int"int"VT\_INT"unsigned 的 int"unsigned int"uint"或"uint32"uint"unsigned 的 int"或"uint"VT\_UINT"bool"bool"bool"boolean"bool"bool"VT\_BOOL"双击"double"double"或"小数"十进制"double"VT\_R8"\_\_int64" \_ \_int64"\_\_int64"或"int64"int64"\_\_int64"VT\_I8"无符号\_ \_int64"无符号\_ \_int64"无符号\_ \_int64"或"uint64"uint64"无符号\_ \_int64"VT\_UI8"DWORD"DWORD"DWORD"uint"大小\_t"大小\_t"NoThrowString"WEX::Common::NoThrowString"XML"WEX::Common::String"XML"字符串"XML"VT\_BSTR
 

注意："String"、"int"、"bool"、"double"，"\_\_int64"，"无符号\_ \_int64"，并可以在"XML"类型中，托管，本机或编写脚本的测试。

默认情况下，如果未指定类型，则假定类型为"String"。 请参阅上面的第一个行。

若要使用上面指定的任何类型跟在指定数组类型，只需追加"\[\]"到类型的末尾。

 

 





