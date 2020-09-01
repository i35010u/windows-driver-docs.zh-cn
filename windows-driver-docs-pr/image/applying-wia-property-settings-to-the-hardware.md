---
title: 将 WIA 属性设置应用到硬件
description: 将 WIA 属性设置应用到硬件
ms.assetid: adb85f77-1814-427b-8b75-0bfce4c8ca06
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c124c048fc2d9abdb06a3ca1f16ccd015cb856bc
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192735"
---
# <a name="applying-wia-property-settings-to-the-hardware"></a>将 WIA 属性设置应用到硬件





当 WIA 应用程序启动数据传输时，WIA 服务会为 WIA 微型驱动程序提供应用当前 WIA 属性设置的机会，并向硬件应用任何特定于设备的设置。 WIA 服务在调用[**IWiaMiniDrv：:D rvacquireitemdata**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)方法之前，先调用[**IWiaMiniDrv：:d rvwriteitemproperties**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvwriteitemproperties)方法。 仅当 WIA 应用程序启动数据传输时，才会调用后一种方法。 WIA 微型驱动程序应使用 WIA 服务函数读取其自己的驱动程序项树中的属性。

### <a name="implementing-iwiaminidrvdrvwriteitemproperties"></a><a href="" id="implementing-iwiaminidrv-drvwriteitemproperties"></a>实现 IWiaMiniDrv：:d rvWriteItemProperties

WIA 服务在客户端请求数据传输后调用 **IWiaMiniDrv：:D rvwriteitemproperties** 方法。 WIA 服务在调用 [**IWiaMiniDrv：:D rvacquireitemdata**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)之前调用此方法。 WIA 微型驱动程序应在从此方法返回之前提交硬件所需的任何设置。

调用此方法时，WIA 微型驱动程序已提交到执行数据传输。 此时，WIA 服务将会失败任何尝试获取数据的应用程序，同时出现 WIA \_ 错误 \_ 忙错误代码。

下面的示例演示 [**IWiaMiniDrv：:D rvwriteitemproperties**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvwriteitemproperties) 方法的实现：

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

 

