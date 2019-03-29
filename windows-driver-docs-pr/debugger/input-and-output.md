---
title: 输入和输出
description: 输入和输出
ms.assetid: 78e181c1-c577-49ca-910b-d2e8db2495b5
keywords:
- 调试器引擎、 输入和输出
- 输入和输出
- output
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b468aedee74ed0f07e5127eff8fd6bf16ae86a9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563861"
---
# <a name="input-and-output"></a>输入和输出


输入和输出设施[调试器引擎](introduction.md#debugger-engine)可用于交互式调试器操作和日志记录。 命令和响应键入的用户，通常表示输入和输出通常表示向用户显示或发送到日志文件的信息。

调试器引擎维护*输入的流*和一个*输出流*。 输入可请求从输入的流和输出发送到输出流。

当[**输入**](https://msdn.microsoft.com/library/windows/hardware/ff550962)方法调用来请求从该引擎的输入流输入时，引擎将调用所有已注册[输入回调](using-input-and-output.md#input-callbacks)通知他们，它是等待输入。 然后，在等待输入进行输入，通过调用的回调[ **ReturnInput** ](https://msdn.microsoft.com/library/windows/hardware/ff554600)方法。

当输出发送到引擎的输出流时，引擎将调用的已注册[输出回调](using-input-and-output.md#output-callbacks)将输出传递给它们。 当将输出发送到输出流，它可以筛选由客户端对象中;在这种情况下，仅向注册的特定客户端对象的输出回调将接收输出。

到远程客户端以透明方式提供的输入和输出流。 远程客户端可以请求输入并将输出发送到引擎的输入和输出流中，引擎将调用注册远程客户端请求的输入或输出发送到回调。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关使用输入和输出的详细信息，请参阅[使用输入和输出](using-input-and-output.md)。 有关客户端对象的信息和输入和输出回调，请参阅[客户端对象](client-objects.md)。

 

 





