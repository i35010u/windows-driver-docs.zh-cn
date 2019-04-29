---
title: GDL 预处理器指导原则
description: GDL 预处理器指导原则
ms.assetid: dc8450ca-cacc-458c-a05b-8566d04d8bae
keywords:
- 预处理器指令 WDK GDL，准则
- 指令 WDK GDL，源文件预处理器指令
- 源文件 WDK GDL，预处理器指令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec04844e5ff0377c384b21363e3e5101723a19f6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380013"
---
# <a name="gdl-preprocessor-guidelines"></a>GDL 预处理器指导原则


在编写 GDL 预处理器指令时，请使用以下准则：

若要防止意外的后果，GDL 文件的编写器应定义预处理器符号和前缀时遵守以下准则。

永远不会取消任何未显式定义在文件中，并在文件结束之前, 的符号始终未定义任何文件中定义的符号。 换而言之，始终不要更改为您找到它们的符号和前缀堆栈。 如果遵循此原则，永远不会将涉及预处理器的命名空间冲突。

GDL 分析器接口将使客户端可以注入 GDL 文本将被处理之前根 GDL 文件的任意大小的片段。 这次机会将使客户端定义以便分析器可以处理的 GDL 文件的相应部分所需的任何预处理器符号。 此片段可能包含其他 GDL 标准模板或定义标准宏。

**请注意**  当文件是包含在行中，所有预处理器符号时，在主机中定义的前缀在所包含的文件的预处理过程中保持已定义。 因为预编译，全新的分析处理文件的时间创建环境。 因此，为其默认值返回所有符号和前缀。 将处理的文件作为预编译不应从外部没有任何依赖关系或托管文件定义预处理器符号。

 

**请注意**  预处理器指令和宏不受开关/用例构造因为指令之前的任何开关/用例构造单独计算。

 

GDL 预处理器指令中不支持逻辑运算符。 有关如何解决这种情况的详细信息，请参阅[GDL 预处理中的逻辑运算符的问题](problems-with-logical-operators-in-gdl-preprocessing.md)。

 

 




