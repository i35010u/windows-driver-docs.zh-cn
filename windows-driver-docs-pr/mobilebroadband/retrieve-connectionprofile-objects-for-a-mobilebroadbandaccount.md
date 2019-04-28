---
title: 检索 MobileBroadbandAccount 的 ConnectionProfile 对象
description: 检索 MobileBroadbandAccount 的 ConnectionProfile 对象
ms.assetid: 7e612aa5-1627-4ada-971a-a1d04eafeb81
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bac18b4eaba44e6b413c7882018d9c644ee20ab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345327"
---
# <a name="retrieve-connectionprofile-objects-for-a-mobilebroadbandaccount"></a>检索 MobileBroadbandAccount 的 ConnectionProfile 对象


一个[ **ConnectionProfile** ](https://msdn.microsoft.com/library/windows/apps/br207249)对象包含一组属性和方法可用于获取连接、 使用情况和数据计划信息，以建立网络连接。 可以通过使用来检索与移动帐户相关联的连接配置文件[ **MobileBroadbandAccount** ](https://msdn.microsoft.com/library/windows/apps/br207353)对象。 下面的代码示例说明了如何执行此操作：

**请注意**  的所有列表[ **ConnectionProfile** ](https://msdn.microsoft.com/library/windows/apps/br207249)可以从检索对象[ **Windows.Networking.Connectivity.NetworkInformation.GetConnectionProfiles**](https://msdn.microsoft.com/library/windows/apps/br207294)。

 

``` syntax
var myConnectionProfileList = myNetworkAccountObject.getConnectionProfiles();

if (myConnectionProfileList.length !== 0)
{
  for (var i = 0; i < myConnectionProfileList.length; i++)
  {
    //Display connection profile properties
    var connectivityLevel = myConnectionProfileList[i].getNetworkConnectivityLevel();
    }
  }
else 
{
  // No connection profiles are associated with this mobile broadband account.
}
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 Api 的常见任务](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






