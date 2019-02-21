---
title: 创建 MobileBroadbandNetwork 对象
description: 创建 MobileBroadbandNetwork 对象
ms.assetid: b69c72dc-56cd-4358-9eae-3859705488ea
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7781b7f9693d7fd401202dcaf0467badddb7a40
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547011"
---
# <a name="create-a-mobilebroadbandnetwork-object"></a>创建 MobileBroadbandNetwork 对象


[**MobileBroadbandNetwork** ](https://msdn.microsoft.com/library/windows/apps/hh770616)对象包含一组可用于获取有关使用移动宽带帐户 （例如，网络注册状态或 APN） 相关联的网络的实时数据的属性。 你可以获取这些对象从[ **MobileBroadbandAccount** ](https://msdn.microsoft.com/library/windows/apps/br207353)仅对象。 请注意，单个**MobileBroadbandAccount**对象可以是关联与多个**MobileBroadbandNetwork**对象，但一次只有一个。 （这将是单一的 SIM 卡，保存 m n O 使用来区分用户帐户的信息，使用在两个不同的移动宽带设备中。）

您获得[ **MobileBroadbandAccount** ](https://msdn.microsoft.com/library/windows/apps/br207353)对象通过获取[ **CurrentNetwork** ](https://msdn.microsoft.com/library/windows/apps/hh770610)属性**MobileBroadbandAccount**对象。 如果没有任何活动的网络时， **CurrentNetwork**读取属性 （例如，因为网络设备已拔掉电源或关闭，或无线电有没有信号），读取此属性将返回 NULL。 因为这可能会随时更改 （例如，用户可以遍历到计算机，电梯导致要删除的连接），我们建议获取属性的副本、 测试的是否为 NULL，并使用该副本。 下面的代码示例阐释了这一点。

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

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[移动宽带 Windows 运行时 Api 的常见任务](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






