---
title: 将项树更改通知给应用程序
description: 将项树更改通知给应用程序
ms.assetid: 6b3cb1d0-ab9f-4895-8c3f-f66c398960bb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eaa1c9568a9154975c92ae5db53a098b3367e55f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378948"
---
# <a name="informing-an-application-of-item-tree-changes"></a>将项树更改通知给应用程序





WIA 设备微型驱动程序必须能够以通知应用程序与 WIA 设备对设备的项树的任何更改的关联。 例如，如果应用程序显示用户界面摄像机上显示的图片的缩略图，WIA 微型驱动程序应该能够通知应用程序的用户界面，则不显示该用户已删除的图片的缩略图。

以下示例实现[ **IWiaMiniDrv::drvDeviceCommand** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdevicecommand)方法演示了如何响应发送给它的 WIA 服务命令并传递到设备命令 WIA 微型驱动程序。 WIA 微型驱动程序将向设备发出命令后，微型驱动程序通知设备项树已更改的应用程序。 在此实现中，该方法确定 WIA 服务已发出"拍照"命令 (WIA\_CMD\_采取\_图片)。 方法调用**TakePicture**方法上根项 （设备项），并通知任何连接的应用程序项树现在包含新的图片。 (这两个 WIA\_CMD\_采取\_图片并**TakePicture** Microsoft Windows SDK 文档中所述。)微型驱动程序将这是通过调用[ **wiasQueueEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasqueueevent)函数。

请注意，当微型驱动程序会发出指示树已更新的事件*所有*侦听应用程序的更改，而不仅仅是调用方会收到通知。 例如，如果用户已打开，照相机的资源管理器视图，并使用 Microsoft 画图来获取新图片，资源管理器窗口还显示了新图片当它到达时，因为它会侦听此类事件。

下面的示例演示的实现**IWiaMiniDrv::drvDeviceCommand**方法。

```cpp
HRESULT _stdcall CWIADevice::drvDeviceCommand(
  BYTE        *pWiasContext,
  LONG        lFlags,
  const GUID  *plCommand,
  IWiaDrvItem **ppWiaDrvItem,
  LONG        *plDevErrVal)
{
  //
  // If the caller did not pass in the correct parameters, 
  // then fail the call and return E_INVALIDARG.
  //

  if ((!pWiasContext)||(!plDevErrVal)||(!plCommand)) {
    return E_INVALIDARG;
  }

  *plDevErrVal = 0;
  HRESULT hr = E_NOTIMPL;

  //
  //  Check which command was issued
  //

  if (*plCommand == WIA_CMD_TAKE_PICTURE) {

    //
    // process command here
    //

      hr = HARDWARE_SNAP_PHOTO();
  }
  return hr;
}
```

 

 




