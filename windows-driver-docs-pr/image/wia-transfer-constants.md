---
title: WIA 传输常量
description: WIA 传输常量
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3eb456dc2a2cfb25b407d7015e08793abd448e46
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826395"
---
# <a name="wia-transfer-constants"></a>WIA 传输常量


本主题包含用于 WIA 基于 **IStream** 的传输的常量的列表。

这些常量分为三个子组：

-   项类型

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
<th>“属性”</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>WiaItemTypeTransfer</strong></p></td>
<td><p>应在能够传输数据的所有项上设置此 <a href="/windows-hardware/drivers/image/wia-ipa-item-flags" data-raw-source="[&lt;strong&gt;WIA_IPA_ITEM_FLAGS&lt;/strong&gt;](./wia-ipa-item-flags.md)"><strong>WIA_IPA_ITEM_FLAGS</strong></a> 位;也就是说，应用程序可以对设置了此位的项启动下载或上传。</p></td>
</tr>
</tbody>
</table>

 

### <a name="callback-messages"></a>回叫消息

下表显示了 **IWiaTransferCallback：： TransferCallback** 的 *lFlags* 参数的可能值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>“属性”</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_STATUS</p></td>
<td><p>通知应用程序传输进度。</p>
<p><em>pWiaTransferParams</em> - pWiaTransferParams &gt;<em>lPercentComplete</em>包含此项和正在传输的页面的完成百分比。</p></td>
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
<p>驱动程序未发送此消息--WIA 服务将在传输结束后自动发送此消息 (即，对 <strong>IWiaMiniDrv：:D rvacquiitemdata</strong> 的调用将返回) 。</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_ERROR</p></td>
<td><p>由 Microsoft 保留以供将来使用。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_DEVICE_STATUS</p></td>
<td><p>指示传输过程中的错误 (例如，卡纸) 。</p>
<p><em>pWiaTransferParams</em> - pWiaTransferParams &gt;<em>hrErrorStatus</em>包含错误状态代码。</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_NEW_PAGE</p></td>
<td><p>指示在多页传输过程中，如果在一个文件中支持多个页面的格式 (如使用多文件 TIFF) ，则将在多页传输过程中传输新页面。</p></td>
</tr>
</tbody>
</table>

 

### <a name="transfer-flags"></a>传输标志

下表显示了可传递到 IWiaMiniDrv 的标志 [**：:D rvacquireitemdata**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>“属性”</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_MINIDRV_TRANSFER_DOWNLOAD</p></td>
<td><p>指示传输是基于流的下载操作 (即从设备到应用程序) 的数据传输。</p>
<p>应用程序不会直接设置此位。 如果应用程序调用 <strong>IWiaTransfer：:D o) </strong>，WIA 服务将设置此位。</p></td>
</tr>
<tr class="even">
<td><p>WIA_MINIDRV_TRANSFER_UPLOAD</p></td>
<td><p>指示传输是基于流的上传操作 (即，将数据从应用程序传输到设备) 。</p>
<p>应用程序不会直接设置此位。 如果应用程序调用 <strong>IWiaTransfer：：上传</strong>，WIA 服务将设置此位。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_MINIDRV_TRANSFER_ACQUIRE_CHILDREN</p></td>
<td><p>指示驱动程序应执行文件夹传输。 如果对某个文件夹项调用此值，则该应用程序将请求传输该文件夹的子文件夹。</p>
<p>如果应用程序通过将<strong>IWiaTransfer：:D o) </strong>的<em>lFlags</em>参数设置为 WIA _TRANSFER_ACQUIRE_CHILDREN 并且驱动程序已指定它可以在一次扫描中传输多个子项<em>，</em>则将设置此值。 如果驱动程序无法执行此类传输，WIA 服务将对驱动程序进行多个调用，并且 <em>不</em> 会设置 WIA_MINIDRV_TRANSFER_ACQUIRE_CHILDREN。</p></td>
</tr>
</tbody>
</table>

 

有关 **IWiaTransfer** 和 **IWiaTransferCallback** 接口的详细信息，请参阅 Microsoft Windows SDK 文档。

