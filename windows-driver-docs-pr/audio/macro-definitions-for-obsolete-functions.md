---
title: 已过时函数的宏定义
description: 已过时函数的宏定义
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 078cb332384248369fb65c05132e305068299008
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801043"
---
# <a name="macro-definitions-for-obsolete-functions"></a>已过时函数的宏定义


## <span id="ddk_macro_definitions_for_obsolete_functions_ks"></span><span id="DDK_MACRO_DEFINITIONS_FOR_OBSOLETE_FUNCTIONS_KS"></span>


标头文件 portcls 定义了多个宏，这些宏有助于编译旧的驱动程序代码，而无需对源文件进行编辑。 这些宏可方便地将对过时 PortCls 和内核模式驱动程序的调用替换为对新的 PortCls 和内核模式驱动程序功能的调用。 如果你有包含对过时函数的引用的旧源代码，则可以使用 portcls 中的宏重新编译源文件，以创建调用新函数的可执行代码。

本文讨论了以下主题：

[已过时端口类函数](obsolete-port-class-functions.md)

[已过时内核模式驱动程序支持函数](obsolete-kernel-mode-driver-support-functions.md)

 

 





