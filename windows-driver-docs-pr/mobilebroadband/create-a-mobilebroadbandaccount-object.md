---
title: 创建 MobileBroadbandAccount 对象
description: 创建 MobileBroadbandAccount 对象
ms.assetid: 631e885f-67bb-4c30-a82f-352c23cc973a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e899d4b14d13736172578f972bd1170a9d80826
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216640"
---
# <a name="create-a-mobilebroadbandaccount-object"></a>创建 MobileBroadbandAccount 对象


由于 [**MobileBroadbandAccount**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount) 对象表示网络帐户，因此创建此类对象需要网络帐户 ID。 从网络列表启动移动宽带应用时，它会接收网络帐户 ID，以用作磁贴启动协定的参数。

如果直接从磁贴激活应用，则不存在与磁贴启动协定关联的参数，必须获取[**MobileBroadbandAccount**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount)类的[**AvailableNetworkAccountIds**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount#Windows_Networking_NetworkOperators_MobileBroadbandAccount_AvailableNetworkAccountIds)静态属性的值。 这会返回字符串的只读集合，其中每个字符串都是一个帐户 ID。 如果此方法返回一个具有单个字符串的集合，则无需执行任何其他操作。 以下 JavaScript 代码示例演示如何执行此操作：

``` syntax
var myNetworkAccountId;
var allNetworkAccountIds = Windows.Networking.NetworkOperators.MobileBroadbandAccount.availableNetworkAccountIds;

if (allNetworkAccountIds.size == 1)
{
  myNetworkAccountId = allNetworkAccountIds[0]; 
}
```

如果返回的集合包含多个字符串，你将需要运行该应用程序的最终用户的输入。 一种方法是循环访问集合，为集合中的每个帐户 ID 创建一个 [**MobileBroadbandAccount**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount) 对象，然后使用对象的属性 (例如，用来填充列表框控件) 的电话号码。 此控件向最终用户提供，用户做出选择后，可以释放所有其他 **MobileBroadbandAccount** 对象。

获得帐户 ID 后，调用[**MobileBroadbandAccount**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount)类的[**CreateFromNetworkAccountId**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount#Windows_Networking_NetworkOperators_MobileBroadbandAccount_CreateFromNetworkAccountId_System_String_)静态方法。 下面的代码示例演示如何使用 JavaScript 执行此操作：

``` syntax
var myNetworkAccountId = "{95499FEF-1579-4547-A0BE-FF271ADBBE76}";
var myNetworkAccountObject = Windows.Networking.NetworkOperators.MobileBroadbandAccount.createFromNetworkAccountId(myNetworkAccountId);
```

## <a name="span-idemptylistspanspan-idemptylistspanmobilebroadbandaccountavailablenetworkaccountids-returns-an-empty-list"></a><span id="emptylist"></span><span id="EMPTYLIST"></span>MobileBroadbandAccount AvailableNetworkAccountIds 返回空列表


如果你的应用程序不受信任，则属性将返回一个空集合，而不是引发异常，因为用户可以在其计算机上拥有多个网络操作员的帐户。 [**AvailableNetworkAccountIds**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount#Windows_Networking_NetworkOperators_MobileBroadbandAccount_AvailableNetworkAccountIds)属性仅返回允许应用的元数据包查看的帐户 id。 由于 **AvailableNetworkAccountIds** 属性检查每个帐户 ID 在检索时是否有与其关联的设备，因此此属性可以返回一个空集合，即使 [**CreateFromNetworkAccountId**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount#Windows_Networking_NetworkOperators_MobileBroadbandAccount_CreateFromNetworkAccountId_System_String_) 不引发访问拒绝异常也是如此。

如果未检测到网络硬件，或者网络硬件没有可访问的 SIM，就会发生这种情况。 若要确定返回的集合为空的确切原因，一种简单的方法是查看 WWAN 日志。 收集日志后，在文本日志文件中搜索包含文本 **AvailableNetworkAccountIds**的条目。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 API 的常见任务]()

 

