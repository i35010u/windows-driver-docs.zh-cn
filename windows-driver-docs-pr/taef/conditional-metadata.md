---
title: 条件元数据
description: 条件元数据
ms.assetid: A1C223AB-E9BB-480e-B9ED-75989FD34479
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f484fc7dcc6bb42489311c1f305b52c88d8455b
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349436"
---
# <a name="conditional-metadata"></a>条件元数据


有时很有用具有元数据值发生更改，具体取决于运行时的值。 条件的元数据允许模块、 类或方法的元数据，仅应用于基于特定条件[运行时参数](runtime-parameters.md)。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


若要使元数据条件，添加条件后的元数据名称用方括号括起来。 条件必须为格式为我们[选择查询语言](selection.md)。 变量的值来自[运行时参数](runtime-parameters.md)。

例如，假设某个测试具有的以下元数据：

```cpp
TEST_METHOD_PROPERTY(L"RunAs", L"Elevated")
TEST_METHOD_PROPERTY(L"Ignore[@NoElevation=true]", L"true")
```

当 TAEF 加载 DLL，则会评估"@NoElevation= true"条件基于运行时参数。 如果用户设置"NoElevation"运行时参数为 true，然后测试将获得对其应用使用"忽略"的名称和值"true"的元数据。

如果多个条件的元数据显示在一个测试，每个是单独计算相同的方式。 这很有用，如果您希望通过测试来识别运行时参数的多个可能的值。

```cpp
TEST_METHOD_PROPERTY(L"Data:MyTestData[@TestCaseLevel='Low']", L"{ Datum1, Datum2, Datum3 }")
TEST_METHOD_PROPERTY(L"DataSource[@TestCaseLevel='High']", L"Pict:FullDataSet.model?Order=3")
```

如果测试具有上面所示的元数据和用户设置为低 TestCaseLevel，测试将只调用三次由于[轻型的数据源](light-weight-data-driven-testing.md)。 如果用户设置为高 TestCaseLevel [PICT 数据源](pict-data-source.md)将用于生成测试的多个参数。 如果 TestCaseLevel 未设置为高或低，则会不添加任何元数据。

## <a name="span-iddefaultspanspan-iddefaultspandefault-values"></a><span id="default"></span><span id="DEFAULT"></span>默认值


当你想要添加元数据，仅当该特定的元数据名称的任何其他条件计算不结果为 true 时，可以将与元数据名称附加*\[默认\]*。

```cpp
TEST_METHOD_PROPERTY(L"DataSource", L"Pict:MyTest.model")
TEST_METHOD_PROPERTY(L"Pict:Order[@TestCaseLevel='Low']", L"1")
TEST_METHOD_PROPERTY(L"Pict:Order[default]", L"2")
TEST_METHOD_PROPERTY(L"Pict:Order[@TestCaseLevel='High']", L"3")
```

如果某个测试具有更高版本的元数据，用户不会设置 TestCaseLevel 为 Low 或高 Pict： 顺序将设置为 2。 如果用户设置 TestCaseLevel 为 Low 或高，Pict： 顺序将设置为 1 或 3，分别。 因为至少一个 Pict： 顺序计算结果为 true 的测试条件，不会应用的值为 2。

请注意，不要丢掉\[默认\]根据需要。

```cpp
TEST_METHOD_PROPERTY(L"DataSource", L"Pict:MyTest.model")
TEST_METHOD_PROPERTY(L"Pict:Order[@TestCaseLevel='Low']", L"1")
TEST_METHOD_PROPERTY(L"Pict:Order", L"2") // This should have [default]
TEST_METHOD_PROPERTY(L"Pict:Order[@TestCaseLevel='High']", L"3")
```

如果 TestCaseLevel 设置为低，设置上述元数据的等效于以下组的元数据：

```cpp
TEST_METHOD_PROPERTY(L"DataSource", L"Pict:MyTest.model")
TEST_METHOD_PROPERTY(L"Pict:Order", L"1")
TEST_METHOD_PROPERTY(L"Pict:Order", L"2")
```

在这种情况下，它是未指定是否 PICT 数据源将使用"1"2"个 PICT 订单。

 

 





