---
title: WIA 传输常量
description: WIA 传输常量
ms.assetid: 69f76919-5bbb-4968-997c-2d51f19aab6b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 973911ef639af6ecbf4ffbb1b7ff1a6135d35c60
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369815"
---
# <a name="wia-transfer-constants"></a>WIA 传输常量


本主题包含一系列用于 WIA 的常量**IStream**-基于传输。

这些常量分为三个子组：

-   项目类型

-   回调消息

-   传输标志

### <a name="item-type"></a>项类型

下表显示哪些 WIA 项键入位与的基于流的数据传输。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>名称</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>WiaItemTypeTransfer</strong></p></td>
<td><p>这<a href="https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-flags" data-raw-source="[&lt;strong&gt;WIA_IPA_ITEM_FLAGS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-flags)"> <strong>WIA_IPA_ITEM_FLAGS</strong> </a>应能够将数据传输的所有项上设置位; 也就是说，应用程序可以启动下载或在项上传，具有此位组。</p></td>
</tr>
</tbody>
</table>

 

### <a name="callback-messages"></a>回调消息

下表显示了可能的值为*lFlags*的参数**IWiaTransferCallback::TransferCallback**。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>名称</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_STATUS</p></td>
<td><p>通知应用程序的传输的进度。</p>
<p><em>pWiaTransferParams</em> - &gt; <em>lPercentComplete</em>包含此项和正在传输的页面的完成百分比。</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_END_OF_STREAM</p></td>
<td><p>有没有更多的数据传输到当前数据流，并且可能会关闭流，请通知应用程序。</p>
<p>新的流随后可能会在多项或多页传输请求。</p>
<p>驱动程序不发送此消息手动-WIA 服务会自动发送此消息时，驱动程序会要求为下一步的流。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_END_OF_TRANSFER</p></td>
<td><p>由传输结束时的应用程序接收。</p>
<p>该驱动程序不会发送此消息--WIA 服务将传输结束后自动发送此消息 (即，调用<strong>IWiaMiniDrv::drvAcquiItemData</strong>返回)。</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_ERROR</p></td>
<td><p>Microsoft 保留供将来使用。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_DEVICE_STATUS</p></td>
<td><p>指示在传输 （例如，纸） 期间出错。</p>
<p><em>pWiaTransferParams</em>-&gt;<em>hrErrorStatus</em>包含的错误状态代码。</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_NEW_PAGE</p></td>
<td><p>表示要在多页传输过程中传输新页面的正在使用一个文件 （如多文件 TIFF) 中支持多个页面的格式时。</p></td>
</tr>
</tbody>
</table>

 

### <a name="transfer-flags"></a>传输标志

下表显示了可能会被传递到的标志[ **IWiaMiniDrv::drvAcquireItemData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>名称</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_MINIDRV_TRANSFER_DOWNLOAD</p></td>
<td><p>指示传输是基于流的下载操作 （即，数据从设备传输到应用程序）。</p>
<p>应用程序不能直接设置此位。 WIA 服务设置此位，如果应用程序调用<strong>IWiaTransfer::Download</strong>。</p></td>
</tr>
<tr class="even">
<td><p>WIA_MINIDRV_TRANSFER_UPLOAD</p></td>
<td><p>指示传输是基于流的上传操作 （即，从设备到应用程序的数据传输）。</p>
<p>应用程序不能直接设置此位。 WIA 服务设置此位，如果应用程序调用<strong>IWiaTransfer::Upload</strong>。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_MINIDRV_TRANSFER_ACQUIRE_CHILDREN</p></td>
<td><p>指示该驱动程序应执行文件夹传输。 如果文件夹项上调用此值，则应用程序请求来传输该文件夹的子级。</p>
<p>将设置此值，如果应用程序通过设置请求文件夹传输<em>lFlags</em>的参数<strong>IWiaTransfer::Download</strong>到 WIA _TRANSFER_ACQUIRE_CHILDREN<em>和</em>驱动程序已指定，但它将在一次扫描多个子级。 如果驱动程序不能执行此类型的传输，WIA 服务将使到驱动程序的多个调用，将 WIA_MINIDRV_TRANSFER_ACQUIRE_CHILDREN<em>不</em>设置。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息**IWiaTransfer**并**IWiaTransferCallback**接口，请参阅 Microsoft Windows SDK 文档。

 

 




