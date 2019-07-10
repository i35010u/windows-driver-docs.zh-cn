---
title: 通过应用程序读取 WIA 项属性
description: 通过应用程序读取 WIA 项属性
ms.assetid: e09f604e-451e-40dc-bc12-a077d4d263ee
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4354291206d0996660b9103cd83949b521f7200
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716831"
---
# <a name="reading-wia-item-properties-by-an-application"></a>通过应用程序读取 WIA 项属性





当应用程序发出请求以读取 WIA 项属性时，WIA 服务调用[ **IWiaMiniDrv::drvReadItemProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvreaditemproperties)方法。

**IWiaMiniDrv::drvReadItemProperties**方法应执行以下任务：

1.  确定所读取的属性是否需要运行更新。 若要确定哪些 WIA 属性在读取，WIA 微型驱动程序可以使用 PROPSPEC 数组 （在 Microsoft Windows SDK 文档中定义）。 建议 WIA 微型驱动程序处理 PROPSPEC 数组之前确定的项类型。 这减少了需要在遍历该数组每个**IWiaMiniDrv::drvReadItemProperties**调用。 如果必须在此设备的子项目上没有运行时属性，只有根项属性读取将处理请求。

2.  通过调用更新当前值[ **wiasWriteMultiple** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritemultiple)或**wiasWriteProp**_Xxx_服务函数，请使用 WIA属性的 id。 这会更新存储在驱动程序项，WIA 属性集和 WIA 服务返回应用程序的新值。

如果 WIA 微型驱动程序不会执行此函数中的任何运行时调整到 WIA 属性，WIA 服务自动仅当前 WIA 属性值返回到应用程序。 此函数仅应该用于属性，例如设备的时钟或需要特定于硬件的检查，如文档送纸器状态的 WIA 属性使用。

### <a href="" id="implementing-iwiaminidrv--drvreaditemproperties-"></a>实现 IWiaMiniDrv::drvReadItemProperties

**IWiaMiniDrv::drvReadItemProperties**时应用程序尝试读取 WIA 项的属性调用方法。 WIA 服务首先通过调用此方法通知驱动程序。 WIA 驱动程序应验证所读取的属性正确。 这是最好访问需要设备状态的属性的硬件 (如[ **WIA\_DPS\_文档\_处理\_状态**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-status)，或[ **WIA\_DPA\_设备\_时间**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dpa-device-time)如果设备支持时钟)。

请务必注意 WIA 驱动程序应与硬件通信仅在少数情况下。 与硬件通信过很多此调用中将显示缓慢和较慢的 WIA 驱动程序。

下面的示例演示的实现[ **IWiaMiniDrv::drvReadItemProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvreaditemproperties)方法：

```cpp
HRESULT _stdcall CWIADevice::drvReadItemProperties(
  BYTE           *pWiasContext,
  LONG           lFlags,
  ULONG          nPropSpec,
  const PROPSPEC *pPropSpec,
  LONG           *plDevErrVal)
{

  //
  // If the caller did not pass in the correct parameters,
  // then fail the call with E_INVALIDARG.
  //

  if (!pWiasContext) {
      return E_INVALIDARG;
  }

  if (!plDevErrVal) {
      return E_INVALIDARG;
  }

  if (!pPropSpec) {
      return E_INVALIDARG;
  }

  *plDevErrVal = 0;

  LONG lWIAItemType = 0;
  HRESULT hr = wiasGetItemType(pWiasContext,&lWIAItemType);
  if(S_OK == hr) {
    //
    // perform custom operations depending on the type of
    // WIA item that was passed to drvReadItemProperties
    //

      if(lWIAItemType & WiaItemTypeRoot) {
      //
      // If the WIA_DPA_CONNECT_STATUS property ID is in the PROPSPEC
      // array, then read the latest "Connect Status".
      // If it is NOT then do nothing. (skip access to the hardware)
      //
      // NOTE: only read properties contained in the PROPSPEC array
      //     from the hardware that need device updates.
      //     If the property in PROPSPEC does not need to be read
      //     from the hardware, or updated, do nothing. The WIA service
      //     will supply the caller with the current value in the
      //     the WIA property set.
      //

          BOOL bReadLatestConnectStatus = FALSE;

      //
      // traverse the WIA PROPSPEC array, looking for known WIA
      // properties that require run-time updates, or needs to be
      // updated with hardware access.
      //

          for(ULONG ulIndex = 0; ulIndex < nPropSpec; ulIndex++) {

        //
        // look for WIA property IDs that really need hardware
        // access, or run-time adjusting.
        //

              if(pPropSpec[ulIndex].propid == WIA_DPA_CONNECT_STATUS) {
                  bReadLatestConnectStatus = TRUE;
              }
          }

        //
        // The item passed in is a ROOT item
        //

         if(bReadLatestConnectStatus) {

            //
            // WIA_DPA_CONNECT_STATUS should be updated from the
            // hardware
            //

 LONG lConnectStatus = HARDWARE_READ_ConnectStatus();

            //
            // update WIA_DPA_CONNECT_STATUS property value using
            // wiasWritePropLong ().  The pWiasContext passed in
            // already represents the current item to be written to.
            //

              hr = wiasWritePropLong(pWiasContext,WIA_DPA_CONNECT_STATUS,lConnectStatus);
              if(S_OK == hr) {

                //
                // The WIA_DPA_CONNECT_STATUS property was successfully updated
                //

              } else {

                //
                //  wiasWritePropLong() failed to write the WIA 
                //  property.  The WIA_DPA_CONNECT_STATUS
                //  property was NOT updated
                //

              }
          }

      } else {

        //
        // The item passed in is any other child item
        //

      }
  } else {

    //
    // wiasGetItemType() failed to get the current item type
    //
  }

  return hr;
}
```

 

 




