---
title: 解锁设备
description: 解锁设备
ms.assetid: 4e6ed725-2384-429b-be1e-027b7784e95b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e684a75e0a55433df0d4a7c1c07a47a65730609
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215282"
---
# <a name="unlock-a-device"></a>解锁设备


移动宽带 API 的一个子集包括 PIN 管理 API。 若要解锁设备，请执行以下操作：

1.  获取帐户设备的网络适配器 ID：

    ``` syntax
    account.currentNetwork.networkAdapter. networkAdapterId
    ```

2.  创建 [**IMbnInterfaceManager**](/windows/desktop/api/mbnapi/nn-mbnapi-imbninterfacemanager) 实例。

3.  向 [**IMbnPinManagerEvents**](/windows/desktop/api/mbnapi/nn-mbnapi-imbnpinmanagerevents) 和 [**IMbnPinEvents**](/windows/desktop/api/mbnapi/nn-mbnapi-imbnpinevents) 连接点建议 (这些点用于获取 PIN 状态和取消阻止/解除锁定) 的结果。 有关详细信息，请参阅 [**IMbnInterfaceManager**](/windows/desktop/api/mbnapi/nn-mbnapi-imbninterfacemanager)的 "备注" 部分。

4.  将网络适配器 ID 传递到 [**IMbnInterfaceManager：： GetInterface**](/windows/desktop/api/mbnapi/nf-mbnapi-imbninterfacemanager-getinterface) 以获取设备的 [**IMbnInterface**](/windows/desktop/api/mbnapi/nn-mbnapi-imbninterface) 接口。

5.  通过调用[**IMbnInterface：： QueryInterface**](/windows/desktop/api/mbnapi/nn-mbnapi-imbninterface)获取设备的[**IMbnPinManager**](/windows/desktop/api/mbnapi/nn-mbnapi-imbnpinmanager)接口。

6.  调用 [**IMbnPinManager：： GetPinState**](/windows/desktop/api/mbnapi/nf-mbnapi-imbnpinmanager-getpinstate) 以获取设备的 PIN 状态 (使用步骤3中注册的连接点) 返回的状态。

7.  通过使用传入事件 [** \_ \_ :p instate**](/windows/desktop/api/mbnapi/ns-mbnapi-mbn_pin_info) 参数，确定设备如何锁定或被阻止。

8.  通过调用 [**IMbnPinManager：： GetPin**](/windows/desktop/api/mbnapi/nf-mbnapi-imbnpinmanager-getpin)获取适当 PIN 的 IMbnPin 接口。

9.  根据设备锁定方式调用 [**IMbnPin：： Enter**](/windows/desktop/api/mbnapi/nf-mbnapi-imbnpin-enter) 或 [**IMbnPin：：解除阻止**](/windows/desktop/api/mbnapi/nf-mbnapi-imbnpin-unblock) (参见步骤 7) 。

10. 通过使用[**IMbnPinEvents**](/windows/desktop/api/mbnapi/nn-mbnapi-imbnpinevents)注册来了解操作是否成功，来侦听**解锁**或**取消阻止**结果。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 API 的常见任务](./create-a-mobilebroadbandaccount-object.md)

 

