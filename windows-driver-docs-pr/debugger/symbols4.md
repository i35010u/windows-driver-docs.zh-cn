---
title: 符号
description: 符号
keywords:
- 调试器引擎，符号
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a805f85243a5ba7c4cdd18830313adc69e53796c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816331"
---
# <a name="symbols"></a>符号


*符号* 是显示在模块中的源文件的命名单元或代码。 有关符号的信息可以包括名称、输入 (（如果适用）) 、地址或寄存器存储位置以及任何父或子符号。 符号的示例包括局部变量和全局) 、函数以及模块中的任何入口点 (变量。

引擎使用符号信息来帮助解释目标中的数据和代码。 使用此信息，引擎可以按名称或位置在内存中搜索符号，并提供符号说明。

引擎从位于本地文件系统或从符号服务器加载的符号文件中获取有关符号的信息。 使用符号服务器时，引擎将自动使用正确版本的符号文件来匹配目标中的模块。 可以在加载相应的模块时加载符号文件，也可以根据需要加载符号文件。

**注意**   通常优化编译器不会在符号文件中包含准确的信息。 这可能会导致引擎误认为某些变量的值，因为可能会错误地描述变量的位置或生存期，导致引擎在 (出现错误的内存块时，或认为变量值为 "处于活动状态" （) ）。 优化编译器还可以更改执行顺序或将函数拆分为多个部分。 最佳结果通常是在调试未优化的代码时获取的。

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关使用符号的详细信息，请参阅 [使用符号](using-symbols.md)。 有关使用符号文件和符号服务器的概述，请参阅本文档的 "调试器" 部分中的 [符号](symbols.md) 。

 

 





