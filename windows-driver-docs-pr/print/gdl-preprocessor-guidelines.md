---
title: GDL 预处理器指导原则
description: GDL 预处理器指导原则
keywords:
- 预处理器指令 WDK GDL，指导原则
- 指令 WDK GDL，源文件预处理器指令
- 源文件 WDK GDL，预处理器指令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61f0bd370a70de8bb9c86590a2b8e769e095984a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796973"
---
# <a name="gdl-preprocessor-guidelines"></a>GDL 预处理器指导原则


编写 GDL 预处理器指令时，请遵循以下准则：

若要防止意外的后果，GDL 文件的编写器在定义预处理器符号和前缀时应遵循以下准则。

永远不要取消定义文件中未显式定义的任何符号，并在文件结束之前始终取消定义在文件中定义的任何符号。 换句话说，在找到符号和前缀堆栈时，始终保留它们。 如果遵循此准则，将永远不会出现涉及预处理器的命名空间冲突。

GDL 分析器接口使客户端能够注入将在根 GDL 文件前处理的任意大小的 GDL 文本片段。 此机会将使客户端能够定义所需的任何预处理器符号，以便分析器处理 GDL 文件的相应部分。 此片段可能包括其他 GDL 标准模板或定义标准宏。

**注意**   如果文件包含在行中，则在对所包含的文件进行预处理期间，主机中定义的所有预处理器符号和前缀仍会定义。 当文件作为预编译处理时，将创建一个全新的分析环境。 因此，所有符号和前缀都将返回到它们的默认值。 将作为预编译处理的文件不应依赖于外部或主机文件定义的预处理器符号。

 

**注意**   预处理器指令和宏不受开关/case 构造的影响，因为在任何开关/case 构造之前都单独计算指令。

 

GDL 预处理器指令中不支持逻辑运算符。 有关解决这种情况的详细信息，请参阅 [GDL 预处理中的逻辑运算符的问题](problems-with-logical-operators-in-gdl-preprocessing.md)。

 

 




