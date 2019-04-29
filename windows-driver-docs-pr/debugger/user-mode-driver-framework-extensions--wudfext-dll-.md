---
title: 用户模式驱动程序框架扩展 (Wudfext.dll)
description: 用户模式驱动程序框架扩展 (Wudfext.dll)
ms.assetid: 56b1c794-5740-44fd-9e5b-691fbfefe5a9
keywords:
- 用户模式驱动程序框架扩展 (wudfext.dll)
- 调试扩展 (wudfext.dll) 的用户模式驱动程序框架
- wudfext.dll （用户模式驱动程序框架扩展）
- 扩展，用户模式驱动程序框架
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56249e09716bfcc09f456404f2c2462b81c7d2bf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368105"
---
# <a name="user-mode-driver-framework-extensions-wudfextdll"></a>用户模式驱动程序框架扩展 (Wudfext.dll)


可用于调试用户模式驱动程序框架驱动程序的扩展命令中 Wudfext.dll 实现。

某些扩展具有 UMDF 是必需的; 的版本的 Windows 版本上的其他限制在单独的参考页上说明了这些限制。

**注意**  在创建新的 KMDF 或 UMDF 驱动程序时，必须选择一个不多于 32 个字符的驱动程序名称。 此长度限制在 wdfglobals.h 中定义。 如果驱动程序名称超过了最大长度，您的驱动程序将无法加载。

 

有关使用这些扩展方法，请参阅[用户模式驱动程序框架调试](user-mode-driver-framework-debugging.md)。

 

 





