---
title: 枚举短信设备
description: 枚举短信设备
ms.assetid: d0d57a4f-df83-4f3b-b7b4-417ad4e11350
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: afe2b3b75d707d015a4c8a90af335c5df112c8af
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216620"
---
# <a name="enumerate-sms-devices"></a>枚举短信设备


移动宽带 SMS 平台提供了获取第一个支持 SMS 的移动宽带设备的功能，或获取所有支持 SMS 的移动宽带设备的列表。 下面的示例代码演示如何使用默认的 SMS 设备和特定设备来实例化 SMS 对象。

**注意**   在 Windows 8、Windows 8.1 或 Windows 10 中使用 c # 或 c + + 的应用程序中，第一次使用[**SmsDevice**](/uwp/api/Windows.Devices.Sms.SmsDevice)对象调用[**GetDefaultAsync**](/uwp/api/Windows.Devices.Sms.SmsDevice#Windows_Devices_Sms_SmsDevice_GetDefaultAsync)或[**FROMIDASYNC**](/uwp/api/Windows.Devices.Sms.SmsDevice#Windows_Devices_Sms_SmsDevice_FromIdAsync_System_String_)时，应在 STA 线程上。 MTA 线程中的调用可能会导致未定义的行为。

 

**使用默认 SMS 设备的 JavaScript 代码示例**

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

**用于枚举所有 SMS 设备的 JavaScript 代码示例**

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

## <a name="span-iddetecterrspanspan-iddetecterrspandetect-sms-device-access-errors"></a><span id="detecterr"></span><span id="DETECTERR"></span>检测 SMS 设备访问错误


你可以检测到枚举 SMS 设备是否失败，因为该应用无法访问 SMS。 如果用户显式拒绝对应用的访问，或者设备元数据未获得对应用的访问权限，则会发生这种情况。

**用于检测 SMS 设备访问错误的 JavaScript 代码示例**

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

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[开发短信应用](developing-sms-apps.md)

 

