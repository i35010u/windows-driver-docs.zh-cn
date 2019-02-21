---
title: 使用客户端对象
description: 使用客户端对象
ms.assetid: 07311a2e-86a7-4985-9dfa-55a876cd7899
keywords:
- 调试器引擎，COM 接口
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2006e9f2686fcd7cb93f656242e486f990c22211
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541588"
---
# <a name="using-client-objects"></a>使用客户端对象


中与调试器引擎进行交互的客户端对象的角色的概述，请参阅[客户端对象](client-objects.md)。

一般情况下，可能只能从在其中创建客户端的线程调用客户端的方法。 通常情况下，从错误的线程调用的方法将立即失败。 此规则值得注意的例外是方法[ **CreateClient**](https://msdn.microsoft.com/library/windows/hardware/ff539320); 此方法可以从任何线程调用，并调用它的线程中返回可用的新客户端。 其他异常都记录在参考部分中。

方法返回一个描述客户端对象的字符串[ **GetIdentity** ](https://msdn.microsoft.com/library/windows/hardware/ff546831) ，也可以编写到引擎的输出流使用[ **OutputIdentity**](https://msdn.microsoft.com/library/windows/hardware/ff553219).

### <a name="span-idcominterfacesspanspan-idcominterfacesspancom-interfaces"></a><span id="com_interfaces"></span><span id="COM_INTERFACES"></span>COM 接口

调试器引擎 API 包含多个 COM 接口; 等它们实现**IUnknown**接口。

一节中描述的接口[调试引擎接口](https://msdn.microsoft.com/library/windows/hardware/ff539131)由客户端实现 （但不一定是最新版本）。 可以使用 COM 方法**iunknown:: Queryinterface**以获取每个这些接口从任何其他人。

客户端实现**IUnknown** COM 接口和将其用于维护引用计数，并选择的接口。 但是，客户端不是已注册的 COM 对象。 该方法**iunknown:: Addref**用于递增对象，并且该方法的引用计数**iunknown:: Release**用于递减引用计数。 当**iunknown:: Queryinterface**调用时，该引用计数会递增，因此，如果不再需要客户端接口指针**iunknown:: Release**应调用要递减引用计数。

当使用创建客户端对象的引用计数将初始化为一个[ **DebugCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff540469)或[ **DebugConnect**](https://msdn.microsoft.com/library/windows/hardware/ff540465)。

请参阅平台 SDK 时，引用计数应为递增和递减有关详细信息。

**Iunknown:: Queryinterface**， **DebugCreate**，和**DebugConnect**每项需要的接口 ID 作为其参数之一。 可以获取 ID，使用此接口 **\_ \_uuidof**运算符。 例如：

```cpp
IDebugClient * debugClient;
HRESULT Hr = DebugCreate( __uuidof(IDebugClient), (void **)&debugClient );
```

**重要**  IDebug\*接口如[ **IDebugEventCallbacks** ](https://msdn.microsoft.com/library/windows/hardware/ff550550)接口，尽管类似，COM 不是正确的 COM Api。 从托管代码中调用这些接口是一个不受支持的方案。 如果使用托管代码调用的接口，例如垃圾回收和线程所有权的问题会导致系统不稳定。

 

 

 





