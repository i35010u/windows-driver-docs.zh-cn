---
title: 将 WIA 属性设置应用到硬件
description: 将 WIA 属性设置应用到硬件
ms.assetid: adb85f77-1814-427b-8b75-0bfce4c8ca06
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c997e2f2227d91e7a869fa0ebba118bf090796b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366769"
---
# <a name="applying-wia-property-settings-to-the-hardware"></a>将 WIA 属性设置应用到硬件





当 WIA 应用程序启动数据传输时，WIA 服务可以允许 WIA 微型驱动程序应用当前 WIA 属性设置，而将任何特定于设备的设置应用到的硬件。 WIA 服务随后将调用[ **IWiaMiniDrv::drvWriteItemProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvwriteitemproperties)方法之前调用[ **IWiaMiniDrv::drvAcquireItemData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)方法。 后一种方法称为 WIA 应用程序启动数据传输时才。 WIA 微型驱动程序应使用 WIA 服务函数来读取其自己的驱动程序项树中的属性。

### <a href="" id="implementing-iwiaminidrv-drvwriteitemproperties"></a>实现 IWiaMiniDrv::drvWriteItemProperties

WIA 服务调用**IWiaMiniDrv::drvWriteItemProperties**方法后的客户端请求数据传输。 WIA 服务调用此方法进行调用之前[ **IWiaMiniDrv::drvAcquireItemData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)。 此方法返回之前，WIA 微型驱动程序应硬件提交其所需的任何设置。

调用此方法时，WIA 微型驱动程序已提交给执行数据传输。 WIA service 会发生故障的任何应用程序尝试获取数据，在这次使用 WIA\_错误\_正忙错误代码。

下面的示例演示的实现[ **IWiaMiniDrv::drvWriteItemProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvwriteitemproperties)方法：

```cpp
HRESULT _stdcall CWIADevice::drvWriteItemProperties(
  BYTE                      *pWiasContext,
  LONG                      lFlags,
  PMINIDRV_TRANSFER_CONTEXT pmdtc,
  LONG                      *plDevErrVal)
{
  //
  // If the caller did not pass in the correct parameters,
  // then fail the call with E_INVALIDARG.
  //

  if (!pWiasContext) {
      return E_INVALIDARG;
  }

 if (!pmdtc) {
      return E_INVALIDARG;
  }

  if (!plDevErrVal) {
      return E_INVALIDARG;
  }

  HRESULT hr = S_OK;
  *plDevErrVal = 0;
  PROPVARIANT pv[2];
  PROPSPEC ps[2] = {
      {PRSPEC_PROPID, WIA_IPS_XRES},
      {PRSPEC_PROPID, WIA_IPS_YRES}
  };

  //
  // initialize propvariant structures
  //

  pv[0].vt = VT_I4;   // X resolution is a LONG value
  pv[1].vt = VT_I4;   // Y resolution is a LONG value

  //
  // read 2 WIA item properties (X and Y resolution)
  //

  hr = wiasReadMultiple(pWiasContext, 2, ps, pv, NULL);

  if (hr == S_OK) {

    //
    // write current X and Y resolution values, read from the
    // the WIA property set, and write them to the device.
    //

      hr = SetMyDeviceXResolution(pv[0].lVal);
      if(S_OK == hr) {
          hr = SetMyDeviceYResolution(pv[1].lVal);
          if(FAILED(hr)) {

            //
            // could not set Y resolution to device
            //

          }
   } else {

        //
        // could not set X resolution to device
        //

      }
  }
  return hr;
}
```

 

 




