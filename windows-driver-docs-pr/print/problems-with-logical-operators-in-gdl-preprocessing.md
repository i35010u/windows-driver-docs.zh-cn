---
title: GDL 预处理中的逻辑运算符的问题
description: GDL 预处理中的逻辑运算符的问题
ms.assetid: 8ba1758c-8b8e-4eb2-8625-ffee213025aa
keywords:
- 预处理器指令 WDK GDL 预处理的问题
- 指令 WDK GDL，源文件预处理器指令
- 源文件 WDK GDL 预处理的问题
- 预处理器指令 WDK GDL，逻辑运算符
- 逻辑运算符 WDK GDL
- NOT 运算符 WDK GDL
- 和 WDK GDL 运算符
- 或运算符 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79ce6bb7e1f9fa21eefb1e2461a53c087ce43450
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533256"
---
# <a name="problems-with-logical-operators-in-gdl-preprocessing"></a>GDL 预处理中的逻辑运算符的问题


当前不支持 GDL 预处理器条件语句中的逻辑运算符，但可以模拟。

### <a href="" id="simulating-the-not-operator"></a> 模拟 NOT 运算符

通常可能如以下代码示例所示使用 NOT 运算符。

```cpp
#Ifdef:  symbol
--do this--
#Endif: 
```

但是，应改为使用下面的代码示例。

```cpp
#Ifdef:  symbol
#Else:
--do this--
#Endif: 
```

### <a href="" id="simulating-the-and-operator"></a> 模拟 AND 运算符

通常可能如以下代码示例所示使用 AND 运算符。

```cpp
#Ifdef:  (symbolA  *AND* symbolB)
--do this--
#Endif: 
```

但是，应改为使用下面的代码示例。

```cpp
#Ifdef:  symbolA
#Ifdef:  symbolB
--do this--
#Endif: 
#Endif: 
```

### <a href="" id="simulating-the-or-operator"></a> 模拟 OR 运算符

通常可能如以下代码示例所示使用 OR 运算符。

```cpp
#Ifdef:  (symbolA  *OR* symbolB)
--do this--
#Endif: 
```

但是，应改为使用下面的代码示例。

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

 

 




