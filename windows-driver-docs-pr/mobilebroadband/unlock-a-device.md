---
title: 解锁设备
description: 解锁设备
ms.assetid: 4e6ed725-2384-429b-be1e-027b7784e95b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 452fe864df1f7dd7d2fa1f72e89025f1f39ac36a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534220"
---
# <a name="unlock-a-device"></a>解锁设备


移动宽带 API 的子集包括 PIN 管理 API。 若要解锁设备，执行以下操作：

1.  获取帐户设备的网络适配器 ID:

    ``` syntax
    account.currentNetwork.networkAdapter. networkAdapterId
    ```

2.  创建[ **IMbnInterfaceManager** ](https://msdn.microsoft.com/library/windows/desktop/dd430416)实例。

3.  通知[ **IMbnPinManagerEvents** ](https://msdn.microsoft.com/library/windows/desktop/dd323118)并[ **IMbnPinEvents** ](https://msdn.microsoft.com/library/windows/desktop/dd323110)连接点 （这些用于获取 PIN 状态和取消阻止/ 解锁结果）。 有关详细信息，请参阅备注部分[ **IMbnInterfaceManager**](https://msdn.microsoft.com/library/windows/desktop/dd430416)。

4.  传递到的网络适配器 ID [ **IMbnInterfaceManager::GetInterface** ](https://msdn.microsoft.com/library/windows/desktop/dd430420)若要获取[ **IMbnInterface** ](https://msdn.microsoft.com/library/windows/desktop/dd430406)设备接口。

5.  获取[ **IMbnPinManager** ](https://msdn.microsoft.com/library/windows/desktop/dd323117)接口通过调用设备[ **IMbnInterface::QueryInterface**](https://msdn.microsoft.com/library/windows/desktop/dd430406)。

6.  调用[ **IMbnPinManager::GetPinState** ](https://msdn.microsoft.com/library/windows/desktop/dd323123)若要获取的设备 （通过使用在步骤 3 中已注册的连接点返回的状态） PIN 状态。

7.  确定如何在设备是锁定还是通过使用阻止[ **MBN\_PIN\_INFO::pinState** ](https://msdn.microsoft.com/library/windows/desktop/dd323226)传递到该事件的参数。

8.  通过调用适当的 PIN 获取 IMbnPin 接口[ **IMbnPinManager::GetPin**](https://msdn.microsoft.com/library/windows/desktop/dd323121)。

9.  调用[ **IMbnPin::Enter** ](https://msdn.microsoft.com/library/windows/desktop/dd323127)或[ **IMbnPin::Unblock**](https://msdn.microsoft.com/library/windows/desktop/dd323134)根据如何在设备锁定 （请参阅第 7 步）。

10. 侦听**解锁**或**解除阻止**使用结果[ **IMbnPinEvents** ](https://msdn.microsoft.com/library/windows/desktop/dd323110)注册，以了解操作是否成功。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[移动宽带 Windows 运行时 Api 的常见任务](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






