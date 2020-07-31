---
title: 表数据源中的参数类型
description: 表数据源中的参数类型
ms.assetid: 034F171E-716F-4795-9B07-46A109052227
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9fd03548bd9009cfe6fb3208bcfc2da2a7020808
ms.sourcegitcommit: f63852446e614c985a65f599cdfe788bdb0c6089
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2020
ms.locfileid: "87425733"
---
# <a name="parameter-types-in-table-data-sources"></a>表数据源中的参数类型

下表是基于表的数据源中可用的各种参数类型的摘要，以及可用于使数据源文件在本机、托管和脚本测试中兼容的类型字符串。

>[!NOTE]
>"String"、"int"、"bool"、"double"、" \_ \_ int64"、"无符号 \_ \_ INT64" 和 "XML" 类型可用于所有、托管、本机或脚本测试。

默认情况下，如果未指定类型，则假定该类型为 "String"。 请参阅每个表中的第一行。

若要将数组类型与以上指定的任何类型一起指定，只需在该类型的末尾追加 " \[ \] "。

## <a name="for-native-tests"></a>对于本机测试

|ParameterType|LanguageType|
|----|----|
|类似|WEX：： Common：： String|
|整形|int|
|"无符号 int"|unsigned int|
|型|bool|
|仔细|Double|
|" \_ \_ int64"|\_\_int64|
|"无符号 \_ \_ int64"|无符号 \_ \_ int64|
|DWORD|DWORD|
|"size \_ t"|大小 \_ t|
|"NoThrowString"|WEX：： Common：： NoThrowString|
|XML|WEX：： Common：： String|

## <a name="for-managed-tests"></a>对于托管测试

|ParameterType|LanguageType|
|----|----|
|类似|string|
|"Int32" 或 "int"|int|
|"uint" 或 "uint32"|uint|
|"bool" 或 "boolean"|bool|
|"double" 或 "decimal"|Decimal|
|" \_ \_ int64" 或 "int64"|int64|
|"无符号 \_ \_ int64" 或 "uint64"|uint64|
|DWORD|uint|
|XML|string|

## <a name="for-script-tests"></a>对于脚本测试

|ParameterType|LanguageType|
|----|----|
|"String" 或 "BSTR"|VT \_ BSTR|
|整形|VT \_ INT|
|"无符号 int" 或 "uint"|VT \_ UINT|
|型|VT \_ BOOL|
|仔细|VT \_ R8|
|" \_ \_ int64"|VT \_ I8|
|"无符号 \_ \_ int64"|VT \_ UI8|
|XML|VT \_ BSTR|
