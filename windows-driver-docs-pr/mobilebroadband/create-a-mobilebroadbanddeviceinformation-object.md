---
title: 创建 MobileBroadbandDeviceInformation 对象
description: 创建 MobileBroadbandDeviceInformation 对象
ms.assetid: d7f89045-acb5-4b7c-9154-c05e4169490d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b38d9f040331eea5cb272589abbc4678fdc1c8c0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534352"
---
# <a name="create-a-mobilebroadbanddeviceinformation-object"></a>创建 MobileBroadbandDeviceInformation 对象


一个[ **MobileBroadbandDeviceInformation** ](https://msdn.microsoft.com/library/windows/apps/br207361)对象包含一组可用于获取有关移动宽带与相关联的网络设备的移动宽带特定于数据的属性帐户 （例如，固件版本）。 你可以获取这些对象从[ **MobileBroadbandAccount** ](https://msdn.microsoft.com/library/windows/apps/br207353)仅对象。 请注意，单个**MobileBroadbandAccount**对象可以是关联与多个**MobileBroadbandDeviceInformation**对象，但一次只有一个。 （这将是单一的 SIM 卡，保存 m n O 使用来区分用户帐户的信息，使用在两个不同的移动宽带设备中。）

您获得[ **MobileBroadbandDeviceInformation** ](https://msdn.microsoft.com/library/windows/apps/br207361)对象通过获取[ **CurrentDeviceInformation** ](https://msdn.microsoft.com/library/windows/apps/hh770609) 属性[ **MobileBroadbandAccount** ](https://msdn.microsoft.com/library/windows/apps/br207353)对象。 如果没有网络的设备时显示的**CurrentDeviceInformation**读取属性 （例如，因为它已拔掉电源或关闭状态），读取此属性将返回 NULL。 因为这可能会随时更改 （例如，用户可以拔出设备），我们建议获取属性的副本、 测试的是否为 NULL，并使用该副本。 下面的代码示例说明了如何执行此操作：

``` syntax
var myDeviceInfo = myNetworkAccountObject.currentDeviceInformation

if (myDeviceInfo == null)
{
  // no device present, inform user
}
else 
{
  // use myDeviceInfo to get the data you need
}
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[移动宽带 Windows 运行时 Api 的常见任务](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






