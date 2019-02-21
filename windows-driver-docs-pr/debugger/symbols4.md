---
title: 符号
description: 符号
ms.assetid: 7eec815b-f81a-4c0f-b862-6ee31be7ed8f
keywords:
- 调试器引擎符号
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 516dced9ed3291a43dbea785931e1a990c478afd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519625"
---
# <a name="symbols"></a>符号


一个*符号*命名单位的数据或出现在模块中的源文件中的代码。 有关符号的信息可以包括名称、 类型 （如果适用）、 地址或注册存储位置和任何父或子符号。 符号的示例包括 （本地和全局） 的变量、 函数和模块任何入口点。

引擎使用的符号信息以帮助解释数据和目标中的代码。 使用此信息，该引擎可以搜索符号按名称或在内存中的位置，并提供符号的说明。

引擎从本地文件系统上或从符号服务器加载符号文件获取其符号信息。 使用符号服务器时，该引擎将自动使用符号文件的正确版本以匹配目标中的模块。 每当加载相应的模块时，或可以根据需要加载它们，可以加载符号文件。

**请注意**  通常优化编译器不准确的信息中包括的符号文件。 这可能会导致错误地解释为变量的位置的一些变量值的引擎或生存期可能被错误地描述，从而导致要看一下错误一部分内存或认为当死信 （或相反） 时，变量的值是实时的引擎。 还有可能用于优化编译器来更改执行顺序，或将函数拆分为多个部分。 调试未优化的代码时，通常会获得最佳结果。

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关使用符号的详细信息，请参阅[使用符号](using-symbols.md)。 有关使用符号文件和符号服务器的概述，请参阅[符号](symbols.md)此文档的调试器部分中。

 

 





