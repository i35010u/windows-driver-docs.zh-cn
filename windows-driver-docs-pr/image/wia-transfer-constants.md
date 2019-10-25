---
title: WIA 传输常量
description: WIA 传输常量
ms.assetid: 69f76919-5bbb-4968-997c-2d51f19aab6b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53852889e9fea285928d576a3c1935e0b11648c0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840666"
---
# <a name="wia-transfer-constants"></a>WIA 传输常量


本主题包含用于 WIA 基于**IStream**的传输的常量的列表。

这些常量分为三个子组：

-   项目类型

-   回叫消息

-   传输标志

### <a name="item-type"></a>项类型

下表显示了哪些 WIA 项类型位与基于流的数据传输相关。

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
<td><p>应在能够传输数据的所有项上设置此<a href="https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-flags" data-raw-source="[&lt;strong&gt;WIA_IPA_ITEM_FLAGS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-flags)"><strong>WIA_IPA_ITEM_FLAGS</strong></a>位;也就是说，应用程序可以对设置了此位的项启动下载或上传。</p></td>
</tr>
</tbody>
</table>

 

### <a name="callback-messages"></a>回叫消息

下表显示了**IWiaTransferCallback：： TransferCallback**的*lFlags*参数的可能值。

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
<td><p>通知应用程序传输进度。</p>
<p><em>pWiaTransferParams</em>-&gt; <em>lPercentComplete</em>包含此项和正在传输的页面的完成百分比。</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_END_OF_STREAM</p></td>
<td><p>通知应用程序没有更多的数据要传输到当前数据流，并且流可能已关闭。</p>
<p>以后可以在多项或多页传输中请求新流。</p>
<p>驱动程序不会手动发送此消息-当驱动程序要求下一个流时，WIA 服务将自动发送此消息。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_END_OF_TRANSFER</p></td>
<td><p>在传输结束时由应用程序接收。</p>
<p>驱动程序未发送此消息--WIA 服务将在传输结束后自动发送此消息（即，对<strong>IWiaMiniDrv：:D rvacquiitemdata</strong>的调用）。</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_ERROR</p></td>
<td><p>由 Microsoft 保留以供将来使用。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_DEVICE_STATUS</p></td>
<td><p>指示传输过程中出现错误（例如卡纸）。</p>
<p><em>pWiaTransferParams</em>-&gt;<em>hrErrorStatus</em>包含错误状态代码。</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_NEW_PAGE</p></td>
<td><p>指示在使用一种文件中支持多个页面的格式（例如多文件 TIFF）时，将在多页传输过程中传输新页。</p></td>
</tr>
</tbody>
</table>

 

### <a name="transfer-flags"></a>传输标志

下表显示了可传递到 IWiaMiniDrv 的标志[ **：:D rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)。

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
<td><p>指示传输是基于流的下载操作（即从设备到应用程序的数据传输）。</p>
<p>应用程序不会直接设置此位。 如果应用程序调用<strong>IWiaTransfer：:D o)</strong>，WIA 服务将设置此位。</p></td>
</tr>
<tr class="even">
<td><p>WIA_MINIDRV_TRANSFER_UPLOAD</p></td>
<td><p>指示传输是基于流的上载操作（即，从应用程序到设备的数据传输）。</p>
<p>应用程序不会直接设置此位。 如果应用程序调用<strong>IWiaTransfer：：上传</strong>，WIA 服务将设置此位。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_MINIDRV_TRANSFER_ACQUIRE_CHILDREN</p></td>
<td><p>指示驱动程序应执行文件夹传输。 如果对某个文件夹项调用此值，则该应用程序将请求传输该文件夹的子文件夹。</p>
<p>如果应用程序通过将<strong>IWiaTransfer：:D o)</strong>的<em>lFlags</em>参数设置为 WIA _TRANSFER_ACQUIRE_CHILDREN 来请求文件夹传输，则将设置此值<em>，并且</em>驱动程序已指定它可以在中传输多个子一次扫描。 如果驱动程序无法执行此类传输，WIA 服务将对驱动程序进行多个调用，并且 WIA_MINIDRV_TRANSFER_ACQUIRE_CHILDREN 将<em>不</em>会设置。</p></td>
</tr>
</tbody>
</table>

 

有关**IWiaTransfer**和**IWiaTransferCallback**接口的详细信息，请参阅 Microsoft Windows SDK 文档。

 

 




