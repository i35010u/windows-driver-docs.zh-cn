---
title: 所需的 dbgerr005 私有符号
description: 所需的 dbgerr005 私有符号
ms.assetid: 0e3b9c98-1f02-4fff-9a91-d3a7470df882
keywords:
- dbgerr005
- 私有符号所需 (dbgerr005)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ab67971615c9971fba45d4c27c3c6e8e470a250
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376074"
---
# <a name="dbgerr005-private-symbols-required"></a>dbgerr005:需要专用符号


## <span id="ddk_dbgerr005_dbg"></span><span id="DDK_DBGERR005_DBG"></span>


调试器错误**dbgerr005**显示消息"私有符号 (symbols.pri) 需要。 局部变量" 此错误指示调试器无法执行操作，因为私有符号不存在。

在内核模式调试，调试器需要 Microsoft Windows 的符号。 在用户模式调试，调试器需要符号为目标应用程序，并且通常需要符号为 Windows 以及。

即使最基本的调试，需要一些基本的符号，如函数名称和全局变量。 这些被称为*公共符号*。 如数据结构名称的符号，只有一个对象文件、 本地变量和行号信息中可见的全局变量并不总是必需进行调试，尽管它们是有用的更深入的调试会话。 这些被称为*私有符号*。

许多软件制造商，包括 Microsoft，生成其符号文件的两个版本。 向客户发布的版本包含仅公共符号。 在内部使用的版本包含公钥和私钥的符号。

可以使用公共符号单独执行大多数调试操作。 但是，某些操作-例如，显示本地变量-需要私有符号。 当尝试进行此类的操作和私有符号不可用时，显示此错误消息。

时看到此消息，则通常最好只需继续调试。 你无法获得的信息至关重要，可能不正确地调试目标。

 

 





