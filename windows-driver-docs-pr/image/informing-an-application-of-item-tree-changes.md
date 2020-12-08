---
title: 将项树更改通知给应用程序
description: 将项树更改通知给应用程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c73edc7f839b1605b1993b07a359a8870431c696
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793673"
---
# <a name="informing-an-application-of-item-tree-changes"></a>将项树更改通知给应用程序





WIA 设备的微型驱动程序必须能够将与 WIA 设备关联的应用程序通知给设备的项树。 例如，如果应用程序显示的用户界面显示照相机上图片的缩略图，则 WIA 微型驱动程序应该能够通知应用程序的用户界面不显示用户已删除的图片的缩略图。

下面的 [**IWiaMiniDrv：:D rvdevicecommand**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdevicecommand) 方法的示例实现显示 wia 微型驱动程序可以如何响应 wia 服务发送给它的命令，并将该命令传递到设备。 WIA 微型驱动程序向设备发出命令后，微型驱动程序会向应用程序通知设备项树已更改。 在此实现中，方法确定 WIA 服务已发出 "拍摄图片" 命令 (WIA \_ CMD \_ Take \_) 。 方法对) 的设备 (项调用 **TakePicture** 方法，并通知所有已连接的应用程序，项树现在包含新图片。  (在 \_ \_ \_ Microsoft Windows SDK 文档中介绍了 WIA CMD TAKE 和 **TakePicture** 。 ) 微型驱动程序通过调用 [**wiasQueueEvent**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasqueueevent) 函数实现此功能。

请注意，当微型驱动程序发出指示树已更新的事件时，将会通知 *所有* 侦听应用程序的更改，而不仅仅是调用方。 例如，如果用户打开了相机的 "资源管理器" 视图，并使用 Microsoft "画图" 获取新图片，则 "资源管理器" 窗口还会在其到达时显示新图片，因为它会侦听此类事件。

下面的示例演示 **IWiaMiniDrv：:D rvdevicecommand** 方法的实现。

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

 

