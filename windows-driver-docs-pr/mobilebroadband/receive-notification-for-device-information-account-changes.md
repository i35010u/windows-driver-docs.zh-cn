---
title: 接收有关设备信息帐户更改的通知
description: 接收有关设备信息帐户更改的通知
ms.assetid: 67d96f61-57dc-4e4b-a6c1-5c3da28e8aaf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46c25398737cb6341df9cab93be16c84ae0701f4
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212555"
---
# <a name="receive-notification-for-device-information-account-changes"></a>接收有关设备信息帐户更改的通知


若要接收有关设备信息帐户更改的通知，请使用如下所述的[**MobileBroadbandAccountWatcher**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher)的[**AccountUpdated**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_AccountUpdated)事件：

1.  实例化 [**MobileBroadbandAccountWatcher**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher) 对象。

2.  添加 [**AccountUpdated**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_AccountUpdated) 事件处理程序。

3.  在观察程序上调用 [**Start**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_Start) 。

4.  查询[**AccountUpdated**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_AccountUpdated)事件处理程序中[**MobileBroadbandAccountUpdatedEventArgs**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountUpdatedEventArgs)对象的[**HasDeviceInformationChanged**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountUpdatedEventArgs#Windows_Networking_NetworkOperators_MobileBroadbandAccountUpdatedEventArgs_HasDeviceInformationChanged)属性。

5.  如果设备信息已更改，请查询电话号码的 account [**CurrentDeviceInformation. TelephoneNumbers**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandDeviceInformation#Windows_Networking_NetworkOperators_MobileBroadbandDeviceInformation_TelephoneNumbers) 属性。

    例如：

    ``` syntax
    if (account.currentDeviceInformation.TelephoneNumbers.length > 0)
    {
      // there is now at least one telephone number
    }
    ```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 API 的常见任务](./create-a-mobilebroadbandaccount-object.md)

 

