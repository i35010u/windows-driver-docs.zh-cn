---
title: 将 WIA 属性设置应用到硬件
description: 将 WIA 属性设置应用到硬件
ms.assetid: adb85f77-1814-427b-8b75-0bfce4c8ca06
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc54a559c2405203c396ddc6f16ec4e0463c6f3a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840894"
---
# <a name="applying-wia-property-settings-to-the-hardware"></a>将 WIA 属性设置应用到硬件





当 WIA 应用程序启动数据传输时，WIA 服务会为 WIA 微型驱动程序提供应用当前 WIA 属性设置的机会，并向硬件应用任何特定于设备的设置。 WIA 服务在调用[**IWiaMiniDrv：:D rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)方法之前，先调用[**IWiaMiniDrv：:d rvwriteitemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvwriteitemproperties)方法。 仅当 WIA 应用程序启动数据传输时，才会调用后一种方法。 WIA 微型驱动程序应使用 WIA 服务函数读取其自己的驱动程序项树中的属性。

### <a href="" id="implementing-iwiaminidrv-drvwriteitemproperties"></a>实现 IWiaMiniDrv：:d rvWriteItemProperties

WIA 服务在客户端请求数据传输后调用**IWiaMiniDrv：:D rvwriteitemproperties**方法。 WIA 服务在调用[**IWiaMiniDrv：:D rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)之前调用此方法。 WIA 微型驱动程序应在从此方法返回之前提交硬件所需的任何设置。

调用此方法时，WIA 微型驱动程序已提交到执行数据传输。 由于 wia\_错误\_繁忙错误代码，WIA 服务将失败，此时任何尝试获取数据的应用程序都将失败。

下面的示例演示[**IWiaMiniDrv：:D rvwriteitemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvwriteitemproperties)方法的实现：

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

 

 




