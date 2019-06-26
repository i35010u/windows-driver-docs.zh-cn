---
title: 创建 MobileBroadbandNetwork 对象
description: 创建 MobileBroadbandNetwork 对象
ms.assetid: b69c72dc-56cd-4358-9eae-3859705488ea
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31c0d52c60f82015bccaf731a896bc010fdc845b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358634"
---
# <a name="create-a-mobilebroadbandnetwork-object"></a>创建 MobileBroadbandNetwork 对象


[**MobileBroadbandNetwork** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandNetwork)对象包含一组可用于获取有关使用移动宽带帐户 （例如，网络注册状态或 APN） 相关联的网络的实时数据的属性。 你可以获取这些对象从[ **MobileBroadbandAccount** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount)仅对象。 请注意，单个**MobileBroadbandAccount**对象可以是关联与多个**MobileBroadbandNetwork**对象，但一次只有一个。 （这将是单一的 SIM 卡，保存 m n O 使用来区分用户帐户的信息，使用在两个不同的移动宽带设备中。）

您获得[ **MobileBroadbandAccount** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount)对象通过获取[ **CurrentNetwork** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount#Windows_Networking_NetworkOperators_MobileBroadbandAccount_CurrentNetwork)属性**MobileBroadbandAccount**对象。 如果没有任何活动的网络时， **CurrentNetwork**读取属性 （例如，因为网络设备已拔掉电源或关闭，或无线电有没有信号），读取此属性将返回 NULL。 因为这可能会随时更改 （例如，用户可以遍历到计算机，电梯导致要删除的连接），我们建议获取属性的副本、 测试的是否为 NULL，并使用该副本。 下面的代码示例阐释了这一点。

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

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 Api 的常见任务](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






