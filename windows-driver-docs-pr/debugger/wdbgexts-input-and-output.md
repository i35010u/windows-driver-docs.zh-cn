---
title: WdbgExts 输入和输出
description: WdbgExts 输入和输出
ms.assetid: 5648b509-7bdd-4d2a-947f-db55a8c69100
keywords:
- WdbgExts 扩展中输入
- WdbgExts 扩展输出
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86965d13bba089e951bc55165baab8aa41653d82
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521182"
---
# <a name="wdbgexts-input-and-output"></a>WdbgExts 输入和输出


本主题提供了可以使用 WdbgExts API 执行的方式输入和输出的简要概述。 有关中的输入和输出流的概述[调试器引擎](introduction.md#debugger-engine)，请参阅[输入和输出](input-and-output.md)中[调试器引擎概述](debugger-engine-overview.md)此文档的部分。

该函数[ **dprintf** ](https://msdn.microsoft.com/library/windows/hardware/ff542750)的工作方式类似于标准 C **printf**函数并将打印到调试器的命令窗口的格式化的字符串或更准确地说，带格式的字符串发送到[输出回调](using-input-and-output.md#output-callbacks)。 若要从调试器引擎读取一行输入，使用函数[ **GetInputLine**](https://msdn.microsoft.com/library/windows/hardware/ff546905)。

若要检查的用户启动的中断，请使用[ **CheckControlC**](https://msdn.microsoft.com/library/windows/hardware/ff539072)。 此函数应在循环中，用于确定用户已尝试取消执行的扩展。

功能更强大的输入和输出 API，请参阅[使用输入和输出](using-input-and-output.md)中[使用调试器引擎 API](using-the-debugger-engine-api.md)此文档的部分。

 

 





