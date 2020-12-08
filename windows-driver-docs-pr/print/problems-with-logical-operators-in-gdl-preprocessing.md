---
title: GDL 预处理中的逻辑运算符问题
description: GDL 预处理中的逻辑运算符问题
keywords:
- 预处理器指令 WDK GDL，预处理问题
- 指令 WDK GDL，源文件预处理器指令
- 源文件 WDK GDL，预处理问题
- 预处理器指令 WDK GDL，逻辑运算符
- 逻辑运算符 WDK GDL
- NOT operator WDK GDL
- AND 运算符 WDK GDL
- OR operator WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97cb4b7ba4708b3574ae4088a74d5b19a1ca4831
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807237"
---
# <a name="problems-with-logical-operators-in-gdl-preprocessing"></a>GDL 预处理中的逻辑运算符问题


当前不支持 GDL 预处理器条件中的逻辑运算符，但可以对其进行模拟。

### <a name="simulating-the-not-operator"></a><a href="" id="simulating-the-not-operator"></a> 模拟 NOT 运算符

通常可以使用 NOT 运算符，如下面的代码示例所示。

```cpp
#Ifdef:  symbol
--do this--
#Endif: 
```

但是，你应该改用下面的代码示例。

```cpp
#Ifdef:  symbol
#Else:
--do this--
#Endif: 
```

### <a name="simulating-the-and-operator"></a><a href="" id="simulating-the-and-operator"></a> 模拟和运算符

通常，可以使用和运算符，如下面的代码示例所示。

```cpp
#Ifdef:  (symbolA  *AND* symbolB)
--do this--
#Endif: 
```

但是，你应该改用下面的代码示例。

```cpp
#Ifdef:  symbolA
#Ifdef:  symbolB
--do this--
#Endif: 
#Endif: 
```

### <a name="simulating-the-or-operator"></a><a href="" id="simulating-the-or-operator"></a> 模拟 OR 运算符

通常，可以使用或运算符，如下面的代码示例所示。

```cpp
#Ifdef:  (symbolA  *OR* symbolB)
--do this--
#Endif: 
```

但是，你应该改用下面的代码示例。

```cpp
#Ifdef:  symbolA
#Define: TempSymbol
#Elseifdef: symbolB
#Define: TempSymbol
#Endif: 
#Ifdef:  TempSymbol
--do this--
#Endif: 
#Undefine: TempSymbol
```

 

 




