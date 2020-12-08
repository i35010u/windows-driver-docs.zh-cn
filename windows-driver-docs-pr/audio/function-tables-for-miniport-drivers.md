---
title: 适用于微型端口驱动程序的函数表
description: 适用于微型端口驱动程序的函数表
keywords:
- 函数表 WDK 音频
- 音频微型端口驱动程序 WDK，函数表
- 微型端口驱动程序 WDK 音频、函数表
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cfa9d7d9a99c5d0755957e6c5c62d706bd6358d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784801"
---
# <a name="function-tables-for-miniport-drivers"></a>适用于微型端口驱动程序的函数表


## <span id="function_tables_for_miniport_drivers"></span><span id="FUNCTION_TABLES_FOR_MINIPORT_DRIVERS"></span>


通用微型端口驱动程序的边界 (参阅 [WDM 音频术语](wdm-audio-terminology.md)) 包含函数表。 某些非音频微型端口驱动程序会在注册过程中向端口驱动程序提供函数表，此时微型端口驱动程序会向端口驱动程序通知小型端口驱动程序将需要的上下文结构的大小。 端口驱动程序将函数表复制到某个专用位置，分配上下文结构，并调用函数表中的初始化函数，同时传递指向上下文结构的指针。

同样，音频微型端口驱动程序使用函数表，但它们是静态分配的，不需要由端口驱动程序复制。 端口驱动程序还从指定的池中 ) 内存中检索其上下文 ( "对象"，并将指向函数表的指针安装到上下文中。 由于函数表指针始终是上下文中的第一个字段，因此端口驱动程序只需要一个上下文指针，并且可以通过上下文访问函数表。

这种方法是因为 COM 为创建抽象对象提供了一种经济高效、易于理解的模型。 音频微型端口驱动程序模型利用 COM 和 COM 宣传资料的行业经验。 可以在 C 或 c + + 中实现和使用对象。 还可以使用汇编语言，但仅应在不需要可移植性的情况下使用。

 

 




