---
title: 解锁设备
description: 解锁设备
ms.assetid: 4e6ed725-2384-429b-be1e-027b7784e95b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53025a63733775b0a05406248527680ceb6073d2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357856"
---
# <a name="unlock-a-device"></a>解锁设备


移动宽带 API 的子集包括 PIN 管理 API。 若要解锁设备，执行以下操作：

1.  获取帐户设备的网络适配器 ID:

    ``` syntax
    account.currentNetwork.networkAdapter. networkAdapterId
    ```

2.  创建[ **IMbnInterfaceManager** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbninterfacemanager)实例。

3.  通知[ **IMbnPinManagerEvents** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbnpinmanagerevents)并[ **IMbnPinEvents** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbnpinevents)连接点 （这些用于获取 PIN 状态和取消阻止/ 解锁结果）。 有关详细信息，请参阅备注部分[ **IMbnInterfaceManager**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbninterfacemanager)。

4.  传递到的网络适配器 ID [ **IMbnInterfaceManager::GetInterface** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbninterfacemanager-getinterface)若要获取[ **IMbnInterface** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbninterface)设备接口。

5.  获取[ **IMbnPinManager** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbnpinmanager)接口通过调用设备[ **IMbnInterface::QueryInterface**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbninterface)。

6.  调用[ **IMbnPinManager::GetPinState** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbnpinmanager-getpinstate)若要获取的设备 （通过使用在步骤 3 中已注册的连接点返回的状态） PIN 状态。

7.  确定如何在设备是锁定还是通过使用阻止[ **MBN\_PIN\_INFO::pinState** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/ns-mbnapi-mbn_pin_info)传递到该事件的参数。

8.  通过调用适当的 PIN 获取 IMbnPin 接口[ **IMbnPinManager::GetPin**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbnpinmanager-getpin)。

9.  调用[ **IMbnPin::Enter** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbnpin-enter)或[ **IMbnPin::Unblock**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbnpin-unblock)根据如何在设备锁定 （请参阅第 7 步）。

10. 侦听**解锁**或**解除阻止**使用结果[ **IMbnPinEvents** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbnpinevents)注册，以了解操作是否成功。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 Api 的常见任务](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






