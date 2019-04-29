---
title: 适用于旧版应用程序和 Windows Vista 驱动程序的映射
description: 适用于旧版应用程序和 Windows Vista 驱动程序的映射
ms.assetid: 6f4ebcc7-ecf0-4e0b-bcef-e5b72dc472dc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c7c711bb93cfd9d1b33f55ed46aa2a49f4fb4a3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380386"
---
# <a name="mapping-for-a-legacy-application-and-windows-vista-driver"></a>适用于旧版应用程序和 Windows Vista 驱动程序的映射


本部分介绍如何 Windows Vista 传输消息和数据流映射到旧传输消息和数据流的旧版应用程序需要能够与 Windows Vista 驱动程序时。

### <a name="callback-transfers"></a>回调传输

此表显示了 Windows Vista 驱动程序的回调传输到的消息发送到旧应用程序的消息的映射。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Windows Vista 驱动程序消息</strong></p></td>
<td><p><strong>（后兼容性层转换） 的旧应用程序消息</strong></p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_STATUS</p></td>
<td><p>IT_MSG_STATUS</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_ERROR</p></td>
<td><p>忽略。</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_END_OF_STREAM</p></td>
<td><p>忽略。 此消息始终会对的调用以及<a href="https://msdn.microsoft.com/library/windows/hardware/ff545039" data-raw-source="[&lt;strong&gt;IWiaTransferCallback::GetNextStream&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545039)"> <strong>IWiaTransferCallback::GetNextStream</strong></a>。 不重复的任何消息，这在中实现<strong>GetNextStream</strong>实现相反。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_END_OF_TRANSFER</p></td>
<td><p>IT_MSG_TERMINATION （请注意 WIA_TRANSFER_MSG_END_OF_TRANSFER 不会发送由驱动程序）。</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_DEVICE_STATUS</p></td>
<td><p>如果 hrErrorStatus = = WIA_STATUS_WARMING_UP，兼容性层将使用 IT_STATUS_TRANSFER_FROM_DEVICE IT_MSG_STATUS 发送为了提供一些状态设置为应用程序，以及提供 Windows Vista 应用程序可能会取消传输。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_NEW_PAGE</p></td>
<td><p>忽略。 应永远不会发送由 Windows Vista 驱动程序在这种情况下，由于我们调入 TYMED_FILE 与 Windows Vista 驱动程序。</p></td>
</tr>
<tr class="even">
<td><p><strong>IWiaTransferCallback::GetNextStream</strong></p></td>
<td><p>第一页：IT_MSG_DATA_HEADER</p>
<p>后续页：IT_MSG_NEW_PAGE</p></td>
</tr>
<tr class="odd">
<td><p><strong>IStream::Write</strong></p></td>
<td><p>IT_MSG_DATA</p></td>
</tr>
</tbody>
</table>

 

### <a name="file-transfers"></a>文件传输

此表显示了 Windows Vista 驱动程序的文件传输到的消息发送到旧应用程序的消息的映射。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Windows Vista 驱动程序消息</strong></p></td>
<td><p><strong>（后兼容性层转换） 的旧应用程序消息</strong></p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_STATUS</p></td>
<td><p>IT_MSG_STATUS</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_ERROR</p></td>
<td><p>忽略。</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_END_OF_STREAM</p></td>
<td><p>忽略。 此消息始终会对的调用以及<a href="https://msdn.microsoft.com/library/windows/hardware/ff545039" data-raw-source="[&lt;strong&gt;IWiaTransferCallback::GetNextStream&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545039)"> <strong>IWiaTransferCallback::GetNextStream</strong></a>。 若要避免重复消息，此消息中实现<strong>GetNextStream</strong>实现相反。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_END_OF_TRANSFER</p></td>
<td><p>IT_MSG_TERMINATION （请注意 WIA_TRANSFER_MSG_END_OF_TRANSFER 不会发送由驱动程序）。</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_DEVICE_STATUS</p></td>
<td><p>如果 hrErrorStatus = = WIA_STATUS_WARMING_UP，IT_MSG_STATUS 为了提供一些状态设置为应用程序，以及提供 Windows Vista 应用程序可能会取消传输，与 IT_STATUS_TRANSFER_FROM_DEVICE 一起发送。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_NEW_PAGE</p></td>
<td><p>IT_MSG_NEW_PAGE</p>
<p>注意： 此行为是多页的稍有不同现在文件传输，因为<em>wiasWritePageBufToFile</em>永远不会发送 IT_MSG_NEW_PAGE。</p></td>
</tr>
<tr class="even">
<td><p><strong>IWiaTransferCallback::GetNextStream</strong></p></td>
<td><p>第一页：IT_MSG_FILE_PREVIEW_DATA_HEADER</p>
<p>后续页：错误 （WIA_ERROR_GENERAL_ERROR 传递回驱动程序）。 <strong>IWiaTransferCallback::GetNextStream</strong>因为您仅可以传输页与 TYMED_FILE 和 TYMED_MULTIPAGE_FILE 传输期间，Windows Vista 驱动程序应只调用后只应调用<strong>GetNextStream</strong>后因为所有的页面应进入同一个流。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IStream::Write</strong></p></td>
<td><p>发送任何消息。 对于文件传输，兼容性层不转换任何驱动程序 （图像处理筛选器） 将写入到旧传输消息的数据。 相反，数据只是写入到返回到末尾的传输用户的文件。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息在旧传输消息，请参阅[IWiaMiniDrvCallBack 接口](https://msdn.microsoft.com/library/windows/hardware/ff543943)。

TYMED 常量的详细信息，请参阅[了解 TYMED](understanding-tymed.md)。

**IStream** Microsoft Windows SDK 文档中详细介绍了接口。

 

 




