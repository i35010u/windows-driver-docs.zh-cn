---
title: 使用客户端对象
description: 使用客户端对象
ms.assetid: 07311a2e-86a7-4985-9dfa-55a876cd7899
keywords:
- 调试器引擎，COM 接口
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c8800583b3000544c9f6f469d949ed2bae7e2da
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84533821"
---
# <a name="using-client-objects"></a>使用客户端对象


有关与调试器引擎交互的客户端对象角色的概述，请参阅[客户端对象](client-objects.md)。

通常，只能从创建客户端的线程调用客户端的方法。 通常，从错误的线程调用的方法会立即失败。 此规则的明显例外是方法[**CreateClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createclient);此方法可从任何线程调用，并返回一个新的客户端，该客户端可用于调用它的线程。 其他异常记录在参考部分。

描述客户端对象的字符串由方法[**GetIdentity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-getidentity)返回，或者可以使用[**OutputIdentity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-outputidentity)写入引擎的输出流。

### <a name="span-idcom_interfacesspanspan-idcom_interfacesspancom-interfaces"></a><span id="com_interfaces"></span><span id="COM_INTERFACES"></span>COM 接口

调试器引擎 API 包含几个 COM，如接口;它们实现**IUnknown**接口。

[调试引擎接口](client-com-interfaces.md)部分中描述的接口是由客户端实现的（尽管不一定是最新版本）。 您可以使用 COM 方法**IUnknown：： QueryInterface**从任何其他接口获取其中的每个接口。

客户端实现**IUnknown** COM 接口，并使用它来维护引用计数和接口选择。 但是，客户端不是已注册的 COM 对象。 方法**iunknown：： AddRef**用于递增对象的引用计数，而方法**Iunknown：： Release**用于递减引用计数。 当调用**iunknown：： QueryInterface**时，引用计数会递增，因此，当不再需要客户端接口指针时，应调用**release**来递减引用计数。

当使用[**DebugCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-debugcreate)或[**DebugConnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-debugconnect)创建客户端对象时，引用计数将被初始化为一个。

有关何时应增加和减少引用计数的详细信息，请参阅平台 SDK。

**IUnknown：： QueryInterface**、 **DebugCreate**和**DebugConnect** ，每个都采用接口 ID 作为其参数之一。 可使用** \_ \_ uuidof**运算符获取此接口 ID。 例如：

```cpp
IDebugClient * debugClient;
HRESULT Hr = DebugCreate( __uuidof(IDebugClient), (void **)&debugClient );
```

**重要提示**   IDebug \* 接口（如 COM like）不是正确的 Com api，如[**IDebugEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugeventcallbacks)接口。 从托管代码调用这些接口是不受支持的方案。 当通过托管代码调用这些接口时，会导致系统不稳定的问题，例如垃圾回收和线程所有权。

 

 

 





