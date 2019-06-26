---
title: 接收有关设备信息帐户更改的通知
description: 接收有关设备信息帐户更改的通知
ms.assetid: 67d96f61-57dc-4e4b-a6c1-5c3da28e8aaf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94def6e8a508d9801bb71febf9017e5718e10134
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369205"
---
# <a name="receive-notification-for-device-information-account-changes"></a>接收有关设备信息帐户更改的通知


若要接收通知的设备信息帐户更改，请使用[ **AccountUpdated** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_AccountUpdated)的事件[ **MobileBroadbandAccountWatcher** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher)如下所述：

1.  实例化[ **MobileBroadbandAccountWatcher** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher)对象。

2.  添加[ **AccountUpdated** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_AccountUpdated)事件处理程序。

3.  调用[**启动**](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_Start)上观察程序。

4.  查询[ **HasDeviceInformationChanged** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountUpdatedEventArgs#Windows_Networking_NetworkOperators_MobileBroadbandAccountUpdatedEventArgs_HasDeviceInformationChanged)属性[ **MobileBroadbandAccountUpdatedEventArgs** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountUpdatedEventArgs)中对象[**AccountUpdated** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_AccountUpdated)事件处理程序。

5.  如果设备信息已更改，查询帐户[ **CurrentDeviceInformation.TelephoneNumbers** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandDeviceInformation#Windows_Networking_NetworkOperators_MobileBroadbandDeviceInformation_TelephoneNumbers)的电话号码的属性。

    例如：

    ``` syntax
    if (account.currentDeviceInformation.TelephoneNumbers.length > 0)
    {
      // there is now at least one telephone number
    }
    ```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 Api 的常见任务](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






