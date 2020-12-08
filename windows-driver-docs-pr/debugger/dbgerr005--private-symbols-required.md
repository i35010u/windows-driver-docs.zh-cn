---
title: 需要 dbgerr005 私有符号
description: 需要 dbgerr005 私有符号
keywords:
- dbgerr005
- 需要 (dbgerr005) 的私有符号
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c729db55bcd98f840a2c6e0df5011f19b3a0d8e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831587"
---
# <a name="dbgerr005-private-symbols-required"></a>dbgerr005:需要专用符号


## <span id="ddk_dbgerr005_dbg"></span><span id="DDK_DBGERR005_DBG"></span>


调试器错误 **dbgerr005** 显示消息 "Private 符号 (符号。) 对于局部变量是必需的。" 此错误表示调试器无法执行操作，因为没有私有符号。

在内核模式调试期间，调试器需要 Microsoft Windows 的符号。 在用户模式调试过程中，调试器需要目标应用程序的符号，并且通常还需要适用于 Windows 的符号。

即使是最基本的调试，也需要一些基本符号，如函数名称和全局变量。 它们称为 *公共符号*。 尽管它们对于更深入的调试会话很有用，但这些符号（例如数据结构名称、只能在一个对象文件、局部变量和行号信息中看到的全局变量）不一定需要用于调试。 它们称为 *私有符号*。

许多软件制造商（包括 Microsoft）都生成其符号文件的两个版本。 向客户发布的版本仅包含公共符号。 内部使用的版本包含公共和私有符号。

大多数调试操作都可以独立于公共符号执行。 但某些操作（如显示局部变量）需要私有符号。 如果尝试执行此类操作且私有符号不可用，则会显示此错误消息。

出现此消息时，通常最好是继续调试。 无法获取的信息可能不是正确调试目标所必需的。

 

 





