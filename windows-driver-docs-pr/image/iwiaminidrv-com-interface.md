---
title: IWiaMiniDrv COM 接口
ms.assetid: a4bd0dee-fb40-42d4-a235-9dab3bc84017
description: 本主题提供了在使用 IWiaMiniDrv COM 接口的详细的指导
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bab076da873671ca8d32a45ae0cdfc6c59932af
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378879"
---
# <a name="iwiaminidrv-com-interface"></a>IWiaMiniDrv COM 接口

图像处理应用程序发出请求到 WIA 服务，后者反过来会与通过微型驱动程序编写器实现设备微型驱动程序进行通信[IWiaMiniDrv 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)。 应用程序通常发出请求：

- [创建并初始化项目](#creating-and-initializing-items)
- [删除项](#deleting-items)
- [枚举设备功能](#enumerating-device-capabilities)
- [枚举图像格式](#enumerating-image-formats)
- [设备命令](#issuing-device-commands)
- [锁定和解锁设备](#locking-and-unlocking-a-device)
- [通知事件的设备](#notifying-a-device-of-an-event)
- [获取设备的错误字符串](#obtaining-device-error-strings)
- [读取和存储项属性](#reading-and-storing-item-properties)
- [将数据传输](#transferring-data)

应用程序到 WIA 服务通过 WIA 应用程序编程接口 (API) 发出请求。 有关此接口的详细信息，请参阅 Microsoft Windows SDK 文档。

**IWiaMiniDrv**接口提供的 WIA 服务来控制设备的以下表中所示的入口点。 WIA 微型驱动程序必须实现每个**IWiaMiniDrv**方法。 这些入口点定义通过下列**IWiaMiniDrv**方法。

## <a name="creating-and-initializing-items"></a>创建并初始化项目

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvanalyzeitem" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvAnalyzeItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvanalyzeitem)"><strong>IWiaMiniDrv::drvAnalyzeItem</strong></a></p></td>
<td><p>检查项，并如有必要，创建子项。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvInitializeWia&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)"><strong>IWiaMiniDrv::drvInitializeWia</strong></a></p></td>
<td><p>初始化 WIA 微型驱动程序。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinititemproperties" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvInitItemProperties&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinititemproperties)"><strong>IWiaMiniDrv::drvInitItemProperties</strong></a></p></td>
<td><p>初始化驱动程序应用程序项树中每一项的项属性。</p></td>
</tr>
</tbody>
</table>

## <a name="deleting-items"></a>删除项

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdeleteitem" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvDeleteItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdeleteitem)"><strong>IWiaMiniDrv::drvDeleteItem</strong></a></p></td>
<td><p>删除驱动程序的项。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvfreedrvitemcontext" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvFreeDrvItemContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvfreedrvitemcontext)"><strong>IWiaMiniDrv::drvFreeDrvItemContext</strong></a></p></td>
<td><p>释放特定于设备的上下文。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvuninitializewia" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvUnInitializeWia&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvuninitializewia)"><strong>IWiaMiniDrv::drvUnInitializeWia</strong></a></p></td>
<td><p>释放与应用程序项树关联的设备资源。</p></td>
</tr>
</tbody>
</table>

## <a name="enumerating-device-capabilities"></a>枚举设备功能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvGetCapabilities&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)"><strong>IWiaMiniDrv::drvGetCapabilities</strong></a></p></td>
<td><p>报告的事件和支持 WIA 微型驱动程序的命令。</p></td>
</tr>
</tbody>
</table>

## <a name="enumerating-image-formats"></a>枚举图像格式

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetwiaformatinfo" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvGetWiaFormatInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetwiaformatinfo)"><strong>IWiaMiniDrv::drvGetWiaFormatInfo</strong></a></p></td>
<td><p>获取支持的设备的格式和媒体类型。</p></td>
</tr>
</tbody>
</table>

## <a name="issuing-device-commands"></a>设备命令

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdevicecommand" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvDeviceCommand&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdevicecommand)"><strong>IWiaMiniDrv::drvDeviceCommand</strong></a></p></td>
<td><p>向成像设备发出命令。</p></td>
</tr>
</tbody>
</table>

## <a name="locking-and-unlocking-a-device"></a>锁定和解锁设备

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvlockwiadevice" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvLockWiaDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvlockwiadevice)"><strong>IWiaMiniDrv::drvLockWiaDevice</strong></a></p></td>
<td><p>锁访问映像的设备。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvunlockwiadevice" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvUnLockWiaDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvunlockwiadevice)"><strong>IWiaMiniDrv::drvUnLockWiaDevice</strong></a></p></td>
<td><p>取消锁定对成像设备访问。</p></td>
</tr>
</tbody>
</table>

## <a name="notifying-a-device-of-an-event"></a>通知事件的设备

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvNotifyPnPEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)"><strong>IWiaMiniDrv::drvNotifyPnPEvent</strong></a></p></td>
<td><p>指示插事件 WIA 微型驱动程序的响应。</p></td>
</tr>
</tbody>
</table>

## <a name="obtaining-device-error-strings"></a>获取设备的错误字符串

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetdeviceerrorstr" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvGetDeviceErrorStr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetdeviceerrorstr)"><strong>IWiaMiniDrv::drvGetDeviceErrorStr</strong></a></p></td>
<td><p>将设备错误值映射到一个字符串。</p></td>
</tr>
</tbody>
</table>

## <a name="reading-and-storing-item-properties"></a>读取和存储项属性

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvreaditemproperties" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvReadItemProperties&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvreaditemproperties)"><strong>IWiaMiniDrv::drvReadItemProperties</strong></a></p></td>
<td><p>读取驱动程序项属性。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvValidateItemProperties&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)"><strong>IWiaMiniDrv::drvValidateItemProperties</strong></a></p></td>
<td><p>验证驱动程序项属性。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvwriteitemproperties" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvWriteItemProperties&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvwriteitemproperties)"><strong>IWiaMiniDrv::drvWriteItemProperties</strong></a></p></td>
<td><p>将驱动程序项属性写入到设备 （如果需要）。</p></td>
</tr>
</tbody>
</table>

## <a name="transferring-data"></a>将数据传输

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvAcquireItemData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)"><strong>IWiaMiniDrv::drvAcquireItemData</strong></a></p></td>
<td><p>将数据从驱动程序项传输到 WIA 服务。</p></td>
</tr>
</tbody>
</table>
