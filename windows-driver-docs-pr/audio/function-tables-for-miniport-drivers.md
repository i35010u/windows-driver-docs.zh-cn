---
title: 适用于微型端口驱动程序的函数表
description: 适用于微型端口驱动程序的函数表
ms.assetid: 86b8bfa7-0c57-480b-b6f6-7c0214f53773
keywords:
- 函数表 WDK 音频
- 音频的微型端口驱动程序 WDK，函数表
- 微型端口驱动程序 WDK 音频，函数表
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1f4e402221fc9285ca3db9d0f664554d38a83d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333624"
---
# <a name="function-tables-for-miniport-drivers"></a>适用于微型端口驱动程序的函数表


## <span id="function_tables_for_miniport_drivers"></span><span id="FUNCTION_TABLES_FOR_MINIPORT_DRIVERS"></span>


泛型的微型端口驱动程序的上边缘接口 (请参阅[WDM 音频术语](wdm-audio-terminology.md)) 包含函数表。 某些非音频微型端口驱动程序中哪些时间微型端口驱动程序会通知的微型端口驱动程序将需要的上下文结构大小的端口驱动程序的注册过程中提供端口驱动程序将在函数表。 端口驱动程序将函数表复制到某个专用位置、 分配的上下文结构，并在函数表中，将指针传递到上下文结构调用初始化函数。

同样，音频微型端口驱动程序使用函数的表，但以静态方式分配，并且不需要端口驱动程序，可复制。 端口驱动程序还从指定的池检索其上下文 （"对象"） 内存，并安装到函数表的指针到上下文。 由于函数表指针始终是在上下文中的第一个字段，端口驱动程序应仅的上下文指针，可以通过上下文访问函数的表。

采取这种方法，因为 COM 提供可靠、 高效地得到广泛了解用于创建抽象的对象模型。 音频的微型端口驱动程序模型利用 COM 和 COM 宣传资料的正文的行业经验。 可以实现并在 C 中使用对象或C++。 程序集语言也可用，但应仅用于不需要的可移植性。

 

 




