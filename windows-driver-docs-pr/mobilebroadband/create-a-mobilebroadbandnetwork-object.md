---
title: 创建 MobileBroadbandNetwork 对象
description: 创建 MobileBroadbandNetwork 对象
ms.assetid: b69c72dc-56cd-4358-9eae-3859705488ea
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77027ce145b0840bab775f24c13595c7d944c5fe
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216638"
---
# <a name="create-a-mobilebroadbandnetwork-object"></a>创建 MobileBroadbandNetwork 对象


[**MobileBroadbandNetwork**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandNetwork) 对象包含一组属性，这些属性可用于获取与移动宽带帐户关联的网络的实时数据 (例如，网络注册状态或 APN) 。 只能从 [**MobileBroadbandAccount**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount) 对象获取这些对象。 请注意，单个 **MobileBroadbandAccount** 对象可以与多个 **MobileBroadbandNetwork** 对象相关联，但每次只能有一个。  (如果单个 SIM 卡保存 o 用于区分用户帐户的信息，则会发生这种情况。 ) 

可以通过获取**MobileBroadbandAccount**对象的[**CurrentNetwork**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount#Windows_Networking_NetworkOperators_MobileBroadbandAccount_CurrentNetwork)属性来获取[**MobileBroadbandAccount**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount)对象。 如果在读取 **CurrentNetwork** 属性时没有活动的网络 (例如，由于拔出或关闭网络设备，或无线电) 没有信号，则读取此属性将返回 NULL。 因为这可能会随时更改 (例如，用户可以在计算机上进入电梯，导致连接断开) ，我们建议你获取属性的副本，测试该属性是否为 NULL，并使用副本。 下面的代码示例阐释了这一点。

``` syntax
var myNetwork = myNetworkAccountObject.currentNetwork

if (myNetwork == null)
{
  // no network, inform user
}
else
{
  // use myNetwork to get the data you need
}
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 API 的常见任务](./create-a-mobilebroadbandaccount-object.md)

 

