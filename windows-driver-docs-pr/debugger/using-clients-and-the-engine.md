---
title: 使用客户端和引擎
description: 使用客户端和引擎
ms.assetid: 899184f5-334b-4fd1-98ce-64475650ace5
keywords:
- DbgEng 扩展，引擎客户端对象
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01c9392cbf197d3e6b3e849f67eab4628d0c8525
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215674"
---
# <a name="using-clients-and-the-engine"></a>使用客户端和引擎


## <span id="ddk_using_clients_and_the_engine_dbx"></span><span id="DDK_USING_CLIENTS_AND_THE_ENGINE_DBX"></span>


DbgEng 扩展通过客户端对象与 [调试器引擎](introduction.md#debugger-engine) 进行交互。

调用扩展函数时，将向其传递客户端。 扩展函数应将此客户端用于与调试器引擎的所有交互，除非它有特定的原因要使用另一个客户端。

在初始化时，扩展库可能会使用 [**DebugCreate**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-debugcreate)创建自己的客户端对象。 此客户端可用于注册 DLL 中的回调对象。

**注意**   修改传递到扩展函数的客户端时应小心谨慎。 特别是，向此客户端注册回调可能会中断调试器的输入、输出或事件处理。 建议创建新的客户端以注册回调。

 

 

