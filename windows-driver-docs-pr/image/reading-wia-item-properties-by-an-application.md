---
title: 通过应用程序读取 WIA 项属性
description: 通过应用程序读取 WIA 项属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27e96f5e7fc3e48eeea54bf262f6b98004a9807e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783249"
---
# <a name="reading-wia-item-properties-by-an-application"></a>通过应用程序读取 WIA 项属性





当应用程序请求读取 WIA 项属性时，WIA 服务将调用 [**IWiaMiniDrv：:D rvreaditemproperties**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvreaditemproperties) 方法。

**IWiaMiniDrv：:D rvreaditemproperties** 方法应执行以下任务：

1.  确定要读取的属性是否需要运行时更新。 若要确定所读取的 WIA 属性，WIA 微型驱动程序可以使用 Microsoft Windows SDK 文档) 中定义 (。 建议 WIA 微型驱动程序在处理 PROPSPEC 数组之前确定项类型。 这减少了在每个 IWiaMiniDrv 上遍历数组的需要 **：:D rvreaditemproperties** 调用。 如果此设备的子项目上没有运行时属性，则只会处理根项属性读取请求。

2.  使用 WIA 属性的 ID 调用 [**wiasWriteMultiple**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritemultiple) 或 **wiasWriteProp**_Xxx_ 服务函数来更新当前值。 这将更新存储在驱动程序项中的 WIA 属性集，WIA 服务会将新值返回到应用程序。

如果 WIA 微型驱动程序不会对此函数中的 WIA 属性执行任何运行时调整，则 WIA 服务会自动仅将当前 WIA 属性值返回到应用程序。 此函数应仅用于需要硬件特定检查的属性（如设备时钟）或 WIA 属性（如文档送纸器状态）。

### <a name="implementing-iwiaminidrvdrvreaditemproperties"></a><a href="" id="implementing-iwiaminidrv--drvreaditemproperties-"></a>实现 IWiaMiniDrv：:d rvReadItemProperties

当应用程序尝试读取 WIA 项的属性时，将调用 **IWiaMiniDrv：:D rvreaditemproperties** 方法。 WIA 服务首先通过调用此方法通知驱动程序。 WIA 驱动程序应验证正在读取的属性是否正确。 如果设备支持时钟) ，这是访问需要设备状态 (例如 [**wia \_ DPS \_ 文档 \_ 处理 \_ 状态**](./wia-dps-document-handling-status.md)或 [**wia \_ DPA \_ 设备 \_ 时间**](./wia-dpa-device-time.md) 的属性的好地方。

请务必注意，WIA 驱动程序只应在极少数情况下与硬件通信。 在此调用中与硬件通信太大的 WIA 驱动程序会显得缓慢且速度缓慢。

下面的示例演示 [**IWiaMiniDrv：:D rvreaditemproperties**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvreaditemproperties) 方法的实现：

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

 

