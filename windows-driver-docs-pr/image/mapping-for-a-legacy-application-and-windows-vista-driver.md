---
title: 适用于旧版应用程序和 Windows Vista 驱动程序的映射
description: 适用于旧版应用程序和 Windows Vista 驱动程序的映射
ms.assetid: 6f4ebcc7-ecf0-4e0b-bcef-e5b72dc472dc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0dd6c767a100f3b81f915d2bf3102eff175f29b
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105730"
---
# <a name="mapping-for-a-legacy-application-and-windows-vista-driver"></a>适用于旧版应用程序和 Windows Vista 驱动程序的映射


本部分介绍当旧的应用程序需要使用 Windows Vista 驱动程序时，Windows Vista 传输消息和数据流如何映射到传统传输消息和数据流。

### <a name="callback-transfers"></a>回调传输

此表显示了如何将 Windows Vista 驱动程序的回调传输消息映射到发送到旧应用程序的消息。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Windows Vista 驱动程序消息</strong></p></td>
<td><p><strong>兼容层转换后 (旧应用程序消息) </strong></p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_STATUS</p></td>
<td><p>IT_MSG_STATUS</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_ERROR</p></td>
<td><p>已忽略。</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_END_OF_STREAM</p></td>
<td><p>已忽略。 此消息始终与对 <a href="/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwiatransfercallback-getnextstream" data-raw-source="[&lt;strong&gt;IWiaTransferCallback::GetNextStream&lt;/strong&gt;](/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwiatransfercallback-getnextstream)"><strong>IWiaTransferCallback：： GetNextStream</strong></a>的调用一起发送。 不复制任何消息，而是在 <strong>GetNextStream</strong> 实现中实现。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_END_OF_TRANSFER</p></td>
<td><p>IT_MSG_TERMINATION (注意驱动程序) 未发送 WIA_TRANSFER_MSG_END_OF_TRANSFER。</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_DEVICE_STATUS</p></td>
<td><p>如果 hrErrorStatus = = WIA_STATUS_WARMING_UP，则兼容层将使用 IT_STATUS_TRANSFER_FROM_DEVICE 发送 IT_MSG_STATUS，以便向应用程序提供某种状态，并使 Windows Vista 应用程序可以取消传输。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_NEW_PAGE</p></td>
<td><p>已忽略。 在这种情况下，绝不应发送 Windows Vista 驱动程序，因为我们使用 TYMED_FILE 调入 Windows Vista 驱动程序。</p></td>
</tr>
<tr class="even">
<td><p><strong>IWiaTransferCallback：： GetNextStream</strong></p></td>
<td><p>第一页： IT_MSG_DATA_HEADER</p>
<p>后续页面： IT_MSG_NEW_PAGE</p></td>
</tr>
<tr class="odd">
<td><p><strong>IStream：： Write</strong></p></td>
<td><p>IT_MSG_DATA</p></td>
</tr>
</tbody>
</table>

 

### <a name="file-transfers"></a>文件传输

此表显示了如何将 Windows Vista 驱动程序的文件传输消息映射到发送到旧应用程序的消息。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Windows Vista 驱动程序消息</strong></p></td>
<td><p><strong>兼容层转换后 (旧应用程序消息) </strong></p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_STATUS</p></td>
<td><p>IT_MSG_STATUS</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_ERROR</p></td>
<td><p>已忽略。</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_END_OF_STREAM</p></td>
<td><p>已忽略。 此消息始终与对 <a href="/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwiatransfercallback-getnextstream" data-raw-source="[&lt;strong&gt;IWiaTransferCallback::GetNextStream&lt;/strong&gt;](/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwiatransfercallback-getnextstream)"><strong>IWiaTransferCallback：： GetNextStream</strong></a>的调用一起发送。 若要避免重复的消息，则应在 <strong>GetNextStream</strong> 实现中实现此消息。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_END_OF_TRANSFER</p></td>
<td><p>IT_MSG_TERMINATION (注意驱动程序) 未发送 WIA_TRANSFER_MSG_END_OF_TRANSFER。</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_DEVICE_STATUS</p></td>
<td><p>如果 hrErrorStatus = = WIA_STATUS_WARMING_UP，将使用 IT_STATUS_TRANSFER_FROM_DEVICE 发送 IT_MSG_STATUS，以便向应用程序提供某种状态，并使 Windows Vista 应用程序可以取消传输。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_NEW_PAGE</p></td>
<td><p>IT_MSG_NEW_PAGE</p>
<p>注意：此行为与今天的多页面文件传输有些不同，因为 <em>wiasWritePageBufToFile</em> 从不发送 IT_MSG_NEW_PAGE。</p></td>
</tr>
<tr class="even">
<td><p><strong>IWiaTransferCallback：： GetNextStream</strong></p></td>
<td><p>第一页： IT_MSG_FILE_PREVIEW_DATA_HEADER</p>
<p>后续页面：错误 (将 WIA_ERROR_GENERAL_ERROR 传递回驱动程序) 。 <strong>IWiaTransferCallback：： GetNextStream</strong> 只应调用一次，因为只能在 TYMED_MULTIPAGE_FILE 传输过程中传输一个 TYMED_FILE 页面，而 Windows Vista 驱动程序只应调用 <strong>GetNextStream</strong> 一次，因为所有页面都应该进入同一个流。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IStream：： Write</strong></p></td>
<td><p>未发送消息。 对于文件传输，兼容层不会转换驱动程序 (图像处理筛选器) 写入旧传输消息中的任何数据。 相反，数据只是写入到传输结束时返回给用户的文件中。</p></td>
</tr>
</tbody>
</table>

 

有关旧传输消息的详细信息，请参阅 [IWiaMiniDrvCallBack 接口](/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback)。

有关 TYMED 常量的详细信息，请参阅 [了解 TYMED](understanding-tymed.md)。

Microsoft Windows SDK 文档中介绍了 **IStream** 接口。

