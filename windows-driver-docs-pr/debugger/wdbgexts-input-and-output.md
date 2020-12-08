---
title: WdbgExts 输入和输出
description: WdbgExts 输入和输出
keywords:
- WdbgExts 扩展，输入
- WdbgExts 扩展，输出
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca7584683b762b4dea4d595a6717671d0225f39c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787689"
---
# <a name="wdbgexts-input-and-output"></a>WdbgExts 输入和输出


本主题简要概述了如何使用 WdbgExts API 执行输入和输出。 有关[调试器引擎](introduction.md#debugger-engine)中输入和输出流的概述，请参阅本文档的 "[调试器引擎概述](debugger-engine-overview.md)" 部分中的[输入和输出](input-and-output.md)。

函数 [**dprintf**](/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_output_routine) 的工作方式类似于标准 C **printf** 函数，并将格式化的字符串打印到调试器命令窗口或者更准确地说，将格式化的字符串发送到 [输出回调](using-input-and-output.md#output-callbacks)。 若要从调试器引擎读取输入行，请使用函数 [**GetInputLine**](/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getinputline)。

若要检查用户启动的中断，请使用 [**CheckControlC**](/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_check_control_c)。 应在循环中使用此函数来确定用户是否试图取消扩展的执行。

有关更强大的输入和输出 API，请参阅本文档中的使用[调试器引擎 API](using-the-debugger-engine-api.md)使用[输入和输出](using-input-and-output.md)部分。

 

