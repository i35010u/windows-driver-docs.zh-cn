---
title: 输入和输出
description: 输入和输出
ms.assetid: 78e181c1-c577-49ca-910b-d2e8db2495b5
keywords:
- 调试器引擎、输入和输出
- 输入和输出
- output
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 725960871f45f5c962ce4e4166ed32cfcbf8dba4
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216657"
---
# <a name="input-and-output"></a>输入和输出


[调试器引擎](introduction.md#debugger-engine)的输入和输出功能可用于交互式调试器操作和日志记录。 输入通常表示用户键入的命令和响应，输出通常表示向用户显示的信息或发送到日志文件的信息。

调试器引擎维护 *输入流* 和 *输出流*。 可以从输入流请求输入，并将输出发送到输出流。

当调用 [**输入**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol-input) 方法以请求引擎输入流中的输入时，引擎将调用所有注册的 [输入回调](using-input-and-output.md#input-callbacks) 以通知它们正在等待输入。 然后，它会等待输入回调通过调用 [**ReturnInput**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-returninput) 方法提供输入。

当输出发送到引擎的输出流时，引擎将调用向其传递输出的已注册 [输出回调](using-input-and-output.md#output-callbacks) 。 在将输出发送到输出流时，可以通过客户端对象对其进行筛选。在这种情况下，仅向特定客户端对象注册的输出回调将接收输出。

远程客户端可以透明地使用输入流和输出流。 远程客户端可以请求输入并将输出发送到引擎的输入和输出流，引擎将调用向远程客户端注册的回调以请求输入或发送输出。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关使用输入和输出的详细信息，请参阅 [使用输入和输出](using-input-and-output.md)。 有关客户端对象以及输入和输出回调的详细信息，请参阅 [客户端对象](client-objects.md)。

 

