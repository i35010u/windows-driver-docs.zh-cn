---
title: 适用于 Vista 应用程序和旧版驱动程序的映射
description: 适用于 Vista 应用程序和旧版驱动程序的映射
ms.assetid: 176157b0-cc30-467b-95ec-2d25a40c43ab
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96c41af7a3bef2cc1939ca71f4590f4b8e37e033
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191195"
---
# <a name="mapping-for-a-vista-application-and-legacy-driver"></a>适用于 Vista 应用程序和旧版驱动程序的映射


本部分介绍当 Windows Vista 应用程序需要使用旧驱动程序时所使用的映射。 下表描述了 WIA 兼容层如何将旧传输消息和数据流映射到 Windows Vista 传输消息和数据流。

### <a name="callback-transfers"></a>回调传输

下表显示了旧驱动程序的回调传输消息到发送到 Windows Vista 应用程序的消息的映射。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>旧驱动程序传输消息</strong></p></td>
<td><p><strong>兼容层转换后 (Windows Vista 应用程序消息) </strong></p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_DATA</p></td>
<td><p><strong>IStream：： Seek、IStream：： Write</strong>，并将所有运算 WIA_TRANSFER_MSG_STATUS 在一起。</p></td>
</tr>
<tr class="odd">
<td><p>IT_MSG_STATUS</p></td>
<td><p>WIA_TRANSFER_MSG_STATUS</p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_DATA_HEADER</p></td>
<td><p>已忽略。 此消息仅由服务发送，而不是由驱动程序发送，并且不会在此类型的传输过程中发送。</p></td>
</tr>
<tr class="odd">
<td><p>IT_MSG_NEW_PAGE</p></td>
<td><p>已忽略。 此类传输过程中永远不会收到此消息。 旧驱动程序只会在多页传输过程中通过未向 Windows Vista 应用程序公开的 TYMED_CALLBACK 或 TYMED_MULTIPAGE_CALLBACK 发送此项。 兼容性层只 TYMED_MULTIPAGE_FILE 的多页传输。 对于 TYMED_FILE 传输，应用程序将始终一次接收一个页面。</p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_TERMINATION</p></td>
<td><p>此消息仅由服务发送，而不是由驱动程序发送。 兼容层将改为发送 WIA_TRANSFER_MSG_END_OF_STREAM 和 WIA_TRANSFER_MSG_END_OF_TRANSFER。</p></td>
</tr>
<tr class="odd">
<td><p>IT_MSG_FILE_PREVIEW_DATA</p></td>
<td><p>已忽略。 <strong>IStream</strong>传输模型不支持带外数据。</p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_FILE_PREVIEW_DATA_HEADER</p></td>
<td><p>已忽略。 <strong>IStream</strong>传输模型不支持带外数据。</p></td>
</tr>
</tbody>
</table>

 

### <a name="file-transfers"></a>文件传输

下表显示了旧驱动程序的文件传输消息到发送到 Windows Vista 应用程序的消息的映射。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>旧驱动程序传输消息</strong></p></td>
<td><p><strong>兼容层转换后 (Windows Vista 应用程序消息) </strong></p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_DATA</p></td>
<td><p>已忽略。 在文件传输过程中永远不应发送此消息。</p></td>
</tr>
<tr class="odd">
<td><p>IT_MSG_STATUS</p></td>
<td><p>WIA_TRANSFER_MSG_STATUS</p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_DATA_HEADER</p></td>
<td><p>已忽略。 此消息仅由服务 (发送) ，不会在此类型的传输过程中发送。</p></td>
</tr>
<tr class="odd">
<td><p>IT_MSG_NEW_PAGE</p></td>
<td><p>已忽略。 此类传输过程中永远不会收到此消息。 旧驱动程序只会在多页传输过程中通过未向 Windows Vista 应用程序公开的 TYMED_CALLBACK 或 TYMED_MULTIPAGE_CALLBACK 发送此项。 不过，兼容层只 TYMED_MULTIPAGE_FILE 的多页传输。 对于 TYMED_FILE 传输，驱动程序将始终一次接收一个页面。</p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_TERMINATION</p></td>
<td><p>此消息仅由该驱动程序) 发送 (。 兼容层将改为发送 WIA_TRANSFER_MSG_END_OF_STREAM 和 WIA_TRANSFER_MSG_END_OF_TRANSFER。</p></td>
</tr>
<tr class="odd">
<td><p>IT_MSG_FILE_PREVIEW_DATA</p></td>
<td><p>已忽略。 新传输模型不支持带外数据。</p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_FILE_PREVIEW_DATA_HEADER</p></td>
<td><p>已忽略。 新传输模型不支持带外数据。</p></td>
</tr>
</tbody>
</table>

 

有关旧传输消息的详细信息，请参阅 [IWiaMiniDrvCallBack 接口](/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback)。

有关 TYMED 常量的详细信息，请参阅 [了解 TYMED](understanding-tymed.md)。

Microsoft Windows SDK 文档中介绍了 **IStream** 接口。

 

