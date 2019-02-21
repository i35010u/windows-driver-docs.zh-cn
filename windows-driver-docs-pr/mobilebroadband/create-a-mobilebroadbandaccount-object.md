---
title: 创建 MobileBroadbandAccount 对象
description: 创建 MobileBroadbandAccount 对象
ms.assetid: 631e885f-67bb-4c30-a82f-352c23cc973a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 584c976f068c81442206641b065a29c022d10526
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525979"
---
# <a name="create-a-mobilebroadbandaccount-object"></a>创建 MobileBroadbandAccount 对象


因为[ **MobileBroadbandAccount** ](https://msdn.microsoft.com/library/windows/apps/br207353)对象表示的网络帐户、 创建此类对象所需的网络帐户 ID。 移动宽带应用启动时从网络列表，它接收要作为磁贴启动协定的参数使用的网络帐户 ID。

如果直接从其磁贴激活应用程序，则没有磁贴启动协定后，关联的参数，必须获取的值[ **AvailableNetworkAccountIds** ](https://msdn.microsoft.com/library/windows/apps/hh770608)的静态属性[ **MobileBroadbandAccount** ](https://msdn.microsoft.com/library/windows/apps/br207353)类。 这将返回一个只读的字符串，其中每个字符串都是单个帐户 id。 集合 如果此方法返回具有单个字符串的集合，不需要采取任何进一步操作。 以下 JavaScript 代码示例演示如何执行此操作：

``` syntax
var myNetworkAccountId;
var allNetworkAccountIds = Windows.Networking.NetworkOperators.MobileBroadbandAccount.availableNetworkAccountIds;

if (allNetworkAccountIds.size == 1)
{
  myNetworkAccountId = allNetworkAccountIds[0]; 
}
```

如果返回的集合包含多个字符串，则需要从正在运行该应用程序最终用户输入。 一种方法是循环访问集合，创建[ **MobileBroadbandAccount** ](https://msdn.microsoft.com/library/windows/apps/br207353)对象在集合中，每个帐户 id，然后使用对象 （例如，电话号码） 的属性若要填充的列表框控件。 此控件显示给最终用户和用户进行选择，所有其他**MobileBroadbandAccount**可释放对象。

帐户 ID 后，请调用[ **CreateFromNetworkAccountId** ](https://msdn.microsoft.com/library/windows/apps/br207354)类的静态方法[ **MobileBroadbandAccount** ](https://msdn.microsoft.com/library/windows/apps/br207353) 。 下面的代码示例演示如何使用 JavaScript 执行此操作：

``` syntax
var myNetworkAccountId = "{95499FEF-1579-4547-A0BE-FF271ADBBE76}";
var myNetworkAccountObject = Windows.Networking.NetworkOperators.MobileBroadbandAccount.createFromNetworkAccountId(myNetworkAccountId);
```

## <a name="span-idemptylistspanspan-idemptylistspanmobilebroadbandaccountavailablenetworkaccountids-returns-an-empty-list"></a><span id="emptylist"></span><span id="EMPTYLIST"></span>MobileBroadbandAccount.AvailableNetworkAccountIds 返回一个空列表


如果您的应用程序不是受信任的该属性返回空集合而不是引发异常，因为用户可以从多个网络运营商在其计算机上的帐户。 [ **AvailableNetworkAccountIds** ](https://msdn.microsoft.com/library/windows/apps/hh770608)属性返回应用程序的元数据包允许查看这些帐户 Id。 因为**AvailableNetworkAccountIds**属性检查每个帐户 ID 必须检索的时间与之关联的设备，则此属性可返回空集合即使[ **CreateFromNetworkAccountId** ](https://msdn.microsoft.com/library/windows/apps/br207354)不会引发拒绝访问异常。

如果检测不到任何网络硬件，或者如果网络硬件不具有可访问 SIM，可以出现此问题。 确定返回的集合为空的确切原因的简单方法是查看 WWAN 日志。 你已收集日志后，搜索文本日志文件包含文本的条目**AvailableNetworkAccountIds**。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[移动宽带 Windows 运行时 Api 的常见任务](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






