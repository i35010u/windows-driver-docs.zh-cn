---
title: 条件元数据
description: 条件元数据
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca608e21892ebf7f8bc94bb619af78c3940ccff8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790894"
---
# <a name="conditional-metadata"></a>条件元数据


有时，根据运行时值更改元数据值会很有用。 条件元数据允许模块、类或方法元数据仅在特定条件下基于 [运行时参数](runtime-parameters.md)应用。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


若要将元数据设置为条件，请在元数据名称后面添加一个由方括号括起来的条件。 条件的格式必须为 [选择查询语言](selection.md)。 变量的值来自 [运行时参数](runtime-parameters.md)。

例如，假设某个测试具有以下元数据：

```cpp
TEST_METHOD_PROPERTY(L"RunAs", L"Elevated")
TEST_METHOD_PROPERTY(L"Ignore[@NoElevation=true]", L"true")
```

然后，当 TAEF 加载 DLL 时，它将 @NoElevation 基于运行时参数计算 "= true" 条件。 因此，如果用户将 "NoElevation" 运行时参数设置为 true，则测试将使用名称为 "Ignore" 且值为 "true" 的元数据应用于它。

如果一个测试中出现多个条件元数据，则将以相同的方式对每个条件元数据进行单独计算。 如果希望测试识别出运行时参数的多个可能的值，这会很有用。

```cpp
TEST_METHOD_PROPERTY(L"Data:MyTestData[@TestCaseLevel='Low']", L"{ Datum1, Datum2, Datum3 }")
TEST_METHOD_PROPERTY(L"DataSource[@TestCaseLevel='High']", L"Pict:FullDataSet.model?Order=3")
```

如果某个测试具有上面显示的元数据，并且该用户将 TestCaseLevel 设置为 Low，则只会因为 [轻型数据源](light-weight-data-driven-testing.md)对该测试调用三次。 如果用户将 TestCaseLevel 设置为 High，则将使用 [PICT 数据源](pict-data-source.md) 为测试生成更多参数。 如果 TestCaseLevel 未设置为 High 或 Low，则不会添加任何元数据。

## <a name="span-iddefaultspanspan-iddefaultspandefault-values"></a><span id="default"></span><span id="DEFAULT"></span>默认值


如果只想要添加元数据，而该特定元数据名称的任何其他条件的计算结果都不为 true，则可以使用 *\[ 默认 \] 值* 追加元数据名称。

```cpp
TEST_METHOD_PROPERTY(L"DataSource", L"Pict:MyTest.model")
TEST_METHOD_PROPERTY(L"Pict:Order[@TestCaseLevel='Low']", L"1")
TEST_METHOD_PROPERTY(L"Pict:Order[default]", L"2")
TEST_METHOD_PROPERTY(L"Pict:Order[@TestCaseLevel='High']", L"3")
```

如果测试具有上述元数据，并且用户未将 TestCaseLevel 设置为 Low 或 High，则 Pict： Order 将设置为2。 如果用户将 TestCaseLevel 设置为 Low 或 High，则 Pict： Order 将分别设置为1或3。 值2将不适用，因为该测试上至少有一个适用于 Pict 的条件： Order 计算结果为 true。

如果需要，请注意不要保留 \[ 默认值 \] 。

```cpp
TEST_METHOD_PROPERTY(L"DataSource", L"Pict:MyTest.model")
TEST_METHOD_PROPERTY(L"Pict:Order[@TestCaseLevel='Low']", L"1")
TEST_METHOD_PROPERTY(L"Pict:Order", L"2") // This should have [default]
TEST_METHOD_PROPERTY(L"Pict:Order[@TestCaseLevel='High']", L"3")
```

如果 TestCaseLevel 设置为 Low，则上述一组元数据等效于下面的一组元数据：

```cpp
TEST_METHOD_PROPERTY(L"DataSource", L"Pict:MyTest.model")
TEST_METHOD_PROPERTY(L"Pict:Order", L"1")
TEST_METHOD_PROPERTY(L"Pict:Order", L"2")
```

在这种情况下，不指定 PICT 数据源将使用 "1" 或 "2" 作为 PICT 顺序。

 

 





