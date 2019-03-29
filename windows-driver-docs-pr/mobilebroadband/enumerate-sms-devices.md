---
title: 枚举短信设备
description: 枚举短信设备
ms.assetid: d0d57a4f-df83-4f3b-b7b4-417ad4e11350
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2415989df11aba351d28b3a9da915070fd773ac2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561898"
---
# <a name="enumerate-sms-devices"></a>枚举短信设备


移动宽带短信平台提供的功能来获取第一个支持短信的移动宽带设备，或者获取所有支持短信的移动宽带设备的列表。 下面的示例代码显示了实例化的 SMS 对象，与默认短信设备和与特定设备。

**请注意**  使用应用中的C#或在 Windows 8、 Windows 8.1 或 Windows 10 中，首次使用 c + + [ **SmsDevice** ](https://msdn.microsoft.com/library/windows/apps/br206511)对象调用[ **GetDefaultAsync** ](https://msdn.microsoft.com/library/windows/apps/br211915)或[ **FromIdAsync** ](https://msdn.microsoft.com/library/windows/apps/br211914)应为 STA 线程上。 来自 MTA 线程的调用可能导致未定义的行为。

 

**若要使用默认短信设备的 JavaScript 代码示例**

``` syntax
var smsDevice = new Windows.Devices.Sms.SmsDevice.getDefault();

try
{
  var smsDeviceOperation = Windows.Devices.Sms.SmsDevice.getDefaultAsync();
  smsDeviceOperation.done(smsDeviceReceived, errorCallback);
}
catch (err)
{
  // handle error
}
```

**若要枚举所有短信设备的 JavaScript 代码示例**

``` syntax
Windows.Devices.Enumeration.DeviceInformation.findAllAsync(Windows.Devices.Sms.SmsDevice.getDeviceSelector()).then(function (smsdevices) 
{
  if (smsdevices.length > 0)
  {
    // for simplicity we choose the first device
    var smsDeviceId = smsdevices[0].Id;
    var smsDeviceOperation = Windows.Devices.Sms.SmsDevice.fromIdAsync(smsNotificationDetails.deviceId); 
    smsDeviceOperation.done(function (smsDeviceResult)
    {
      smsDevice = smsDeviceResult;
    }, errorCallback);
  }
}
```

## <a name="span-iddetecterrspanspan-iddetecterrspandetect-sms-device-access-errors"></a><span id="detecterr"></span><span id="DETECTERR"></span>检测到 SMS 设备访问错误


你可以检测到如果枚举短信设备失败，因为该应用程序不能访问到短信。 如果用户显式拒绝应用的访问权限或设备元数据未授予应用的访问权限，则可以发生这种情况。

**若要检测的短信设备访问错误的 JavaScript 代码示例**

``` syntax
Windows.Devices.Enumeration.DeviceInformation.findAllAsync(Windows.Devices.Sms.SmsDevice.getDeviceSelector()).then(function (smsdevices)
{
  if (smsdevices.length > 0)
  {
    // for simplicity we choose the first device
    var smsDeviceId = smsdevices[0].Id.slice(startIndex,endIndex + 1);
    var smsDeviceOperation = Windows.Devices.Sms.SmsDevice.fromIdAsync(smsNotificationDetails.deviceId); 
    smsDeviceOperation.done(function (smsDeviceResult)
    {
      smsDevice = smsDeviceResult;
    }, errorCallback); 

    // detect if SMS access is denied due to user not granting app consent to use SMS or if metadata is missing or invalid.

  }

function errorCallback(error)
{
  WinJS.log(error.name + " : " + error.description, "sample", "error");

  // If the error was caused due to access being denied to this app
  // then the HResult is set to E_ACCESSDENIED (0x80007005)

  // var hResult = hex(error.number);

}

function hex(nmb)
{
  if (nmb >= 0)
  {
    return nmb.toString(16);
  }
  else
  {
    return (nmb + 0x100000000).toString(16);
  }
}
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[开发 SMS 应用程序](developing-sms-apps.md)

 

 






