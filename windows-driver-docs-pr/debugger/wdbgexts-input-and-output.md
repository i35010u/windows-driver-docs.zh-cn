---
title: WdbgExts 输入和输出
description: WdbgExts 输入和输出
ms.assetid: 5648b509-7bdd-4d2a-947f-db55a8c69100
keywords:
- WdbgExts 扩展中输入
- WdbgExts 扩展输出
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01825ac56348d7f814e6658eb2ae6fd754b0e729
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369440"
---
# <a name="wdbgexts-input-and-output"></a>WdbgExts 输入和输出


本主题提供了可以使用 WdbgExts API 执行的方式输入和输出的简要概述。 有关中的输入和输出流的概述[调试器引擎](introduction.md#debugger-engine)，请参阅[输入和输出](input-and-output.md)中[调试器引擎概述](debugger-engine-overview.md)此文档的部分。

该函数[ **dprintf** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nc-wdbgexts-pwindbg_output_routine)的工作方式类似于标准 C **printf**函数并将打印到调试器的命令窗口的格式化的字符串或更准确地说，带格式的字符串发送到[输出回调](using-input-and-output.md#output-callbacks)。 若要从调试器引擎读取一行输入，使用函数[ **GetInputLine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-getinputline)。

若要检查的用户启动的中断，请使用[ **CheckControlC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nc-wdbgexts-pwindbg_check_control_c)。 此函数应在循环中，用于确定用户已尝试取消执行的扩展。

功能更强大的输入和输出 API，请参阅[使用输入和输出](using-input-and-output.md)中[使用调试器引擎 API](using-the-debugger-engine-api.md)此文档的部分。

 

 





