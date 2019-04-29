---
title: 已过时函数的宏定义
description: 已过时函数的宏定义
ms.assetid: 3d69b089-4875-4860-b5eb-3b5edcf3fc89
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c08e5bec3f1460f48c08e00065062e8fe4f043d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332395"
---
# <a name="macro-definitions-for-obsolete-functions"></a>已过时函数的宏定义


## <span id="ddk_macro_definitions_for_obsolete_functions_ks"></span><span id="DDK_MACRO_DEFINITIONS_FOR_OBSOLETE_FUNCTIONS_KS"></span>


标头文件 portcls.h 定义宏，帮助了的许多旧驱动程序代码编译而无需对源文件进行编辑。 这些宏可以方便地替换已过时 PortCls 和内核模式驱动程序函数通过调用新 PortCls 和内核模式驱动程序函数的调用。 如果必须包含对已过时的函数的引用的旧源代码，可以在 portcls.h 使用宏进行重新编译源代码文件，以创建调用新函数的可执行代码。

论述了以下主题：

[已过时的端口类函数](obsolete-port-class-functions.md)

[已过时的内核模式驱动程序支持函数](obsolete-kernel-mode-driver-support-functions.md)

 

 





