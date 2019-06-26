---
title: 适用于 Vista 应用程序和旧版驱动程序的映射
description: 适用于 Vista 应用程序和旧版驱动程序的映射
ms.assetid: 176157b0-cc30-467b-95ec-2d25a40c43ab
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 399fc92bd60e01d0f0897ea285ec86ed3e017e4c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378843"
---
# <a name="mapping-for-a-vista-application-and-legacy-driver"></a>适用于 Vista 应用程序和旧版驱动程序的映射


本部分介绍 Windows Vista 应用程序需要使用旧驱动程序时使用的映射。 下表描述了 WIA 兼容性层将旧传输消息和对 Windows Vista 传输消息的数据流和数据流的映射。

### <a name="callback-transfers"></a>回调传输

此表显示了旧驱动程序的回调传输到的消息发送到 Windows Vista 应用程序的消息的映射。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>旧驱动程序传输消息</strong></p></td>
<td><p><strong>Windows Vista 应用程序 （后兼容性层转换） 的消息</strong></p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_DATA</p></td>
<td><p><strong>IStream::Seek、 IStream::Write</strong>，和 WIA_TRANSFER_MSG_STATUS 所有或运算组合在一起。</p></td>
</tr>
<tr class="odd">
<td><p>IT_MSG_STATUS</p></td>
<td><p>WIA_TRANSFER_MSG_STATUS</p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_DATA_HEADER</p></td>
<td><p>忽略。 此消息不是由驱动程序，仅发送由服务，并且不会在这种类型的传输过程中发送。</p></td>
</tr>
<tr class="odd">
<td><p>IT_MSG_NEW_PAGE</p></td>
<td><p>忽略。 永远不应在这种类型的传输期间收到此消息。 旧驱动程序只会发送这在使用 TYMED_CALLBACK 或未公开的 TYMED_MULTIPAGE_CALLBACK 多页传输到 Windows Vista 应用程序。 兼容性层仅执行与 TYMED_MULTIPAGE_FILE 多页传输。 对于 TYMED_FILE 传输模式，将始终在时间中收到一页。</p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_TERMINATION</p></td>
<td><p>此消息只能由服务发送不是由驱动程序。 兼容性层将改为发送 WIA_TRANSFER_MSG_END_OF_STREAM 和 WIA_TRANSFER_MSG_END_OF_TRANSFER。</p></td>
</tr>
<tr class="odd">
<td><p>IT_MSG_FILE_PREVIEW_DATA</p></td>
<td><p>忽略。 <strong>IStream</strong>传输模式不支持带外数据。</p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_FILE_PREVIEW_DATA_HEADER</p></td>
<td><p>忽略。 <strong>IStream</strong>传输模式不支持带外数据。</p></td>
</tr>
</tbody>
</table>

 

### <a name="file-transfers"></a>文件传输

此表显示了旧驱动程序的文件传输到的消息发送到 Windows Vista 应用程序的消息的映射。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>旧驱动程序传输消息</strong></p></td>
<td><p><strong>Windows Vista 应用程序 （后兼容性层转换） 的消息</strong></p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_DATA</p></td>
<td><p>忽略。 此消息应永远不会发送文件传输过程中。</p></td>
</tr>
<tr class="odd">
<td><p>IT_MSG_STATUS</p></td>
<td><p>WIA_TRANSFER_MSG_STATUS</p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_DATA_HEADER</p></td>
<td><p>忽略。 此消息仅由服务发送 （不是由驱动程序），并且不会在这种类型的传输过程中发送。</p></td>
</tr>
<tr class="odd">
<td><p>IT_MSG_NEW_PAGE</p></td>
<td><p>忽略。 永远不应在这种类型的传输期间收到此消息。 旧驱动程序只会发送这在使用 TYMED_CALLBACK 或未公开的 TYMED_MULTIPAGE_CALLBACK 多页传输到 Windows Vista 应用程序。 但是，兼容性层，仅执行与 TYMED_MULTIPAGE_FILE 多页传输。 对于 TYMED_FILE 传输，该驱动程序将始终会收到一页一次。</p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_TERMINATION</p></td>
<td><p>此消息仅由服务发送 （不是由驱动程序）。 WIA_TRANSFER_MSG_END_OF_STREAM 和 WIA_TRANSFER_MSG_END_OF_TRANSFER，将改为发送的兼容性层。</p></td>
</tr>
<tr class="odd">
<td><p>IT_MSG_FILE_PREVIEW_DATA</p></td>
<td><p>忽略。 新的传输模式不支持带外数据。</p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_FILE_PREVIEW_DATA_HEADER</p></td>
<td><p>忽略。 新的传输模式不支持带外数据。</p></td>
</tr>
</tbody>
</table>

 

旧传输消息的详细信息，请参阅[IWiaMiniDrvCallBack 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback)。

TYMED 常量的详细信息，请参阅[了解 TYMED](understanding-tymed.md)。

**IStream** Microsoft Windows SDK 文档中详细介绍了接口。

 

 




