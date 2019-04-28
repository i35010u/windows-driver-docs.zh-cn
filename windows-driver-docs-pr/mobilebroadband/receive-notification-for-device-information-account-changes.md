---
title: 接收有关设备信息帐户更改的通知
description: 接收有关设备信息帐户更改的通知
ms.assetid: 67d96f61-57dc-4e4b-a6c1-5c3da28e8aaf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9732c1c3412adcfe49f419645e0d9220402c87d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335428"
---
# <a name="receive-notification-for-device-information-account-changes"></a>接收有关设备信息帐户更改的通知


若要接收通知的设备信息帐户更改，请使用[ **AccountUpdated** ](https://msdn.microsoft.com/library/windows/apps/hh770601)的事件[ **MobileBroadbandAccountWatcher** ](https://msdn.microsoft.com/library/windows/apps/hh770597)如下所述：

1.  实例化[ **MobileBroadbandAccountWatcher** ](https://msdn.microsoft.com/library/windows/apps/hh770597)对象。

2.  添加[ **AccountUpdated** ](https://msdn.microsoft.com/library/windows/apps/hh770601)事件处理程序。

3.  调用[**启动**](https://msdn.microsoft.com/library/windows/apps/hh770604)上观察程序。

4.  查询[ **HasDeviceInformationChanged** ](https://msdn.microsoft.com/library/windows/apps/hh770594)属性[ **MobileBroadbandAccountUpdatedEventArgs** ](https://msdn.microsoft.com/library/windows/apps/hh770593)中对象[**AccountUpdated** ](https://msdn.microsoft.com/library/windows/apps/hh770601)事件处理程序。

5.  如果设备信息已更改，查询帐户[ **CurrentDeviceInformation.TelephoneNumbers** ](https://msdn.microsoft.com/library/windows/apps/br207373)的电话号码的属性。

    例如：

    ``` syntax
    if (account.currentDeviceInformation.TelephoneNumbers.length > 0)
    {
      // there is now at least one telephone number
    }
    ```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 Api 的常见任务](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






