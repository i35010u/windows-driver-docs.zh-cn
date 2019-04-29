---
title: Wi-Fi 直接打印
description: Windows 8.1 和更高版本的 Windows 支持通过 Wi-Fi Direct (WFD) 打印。
ms.assetid: B2FC1293-F9E4-43A4-84BF-21EF8C3D27E0
ms.date: 01/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 22ef2a07b95369716d567bb4bfd4c8d3cb94ca63
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370387"
---
# <a name="wi-fi-direct-printing"></a>Wi-Fi 直接打印


Windows 8.1 和更高版本的 Windows 支持通过 Wi-Fi Direct (WFD) 打印。

实现 Windows Wi-Fi Direct 支持用于打印的打印设备必须实现以下功能：

-   Wi-Fi Direct 垂直配对
-   与容器 ID 匹配的物理设备中的所有逻辑设备
-   WSD/WS-Print

使用本主题及其副主题中的定义：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>术语</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WFD</p></td>
<td><p>WLAN Direct</p></td>
</tr>
<tr class="even">
<td><p>DAF</p></td>
<td><p>设备关联框架</p></td>
</tr>
<tr class="odd">
<td><p>DAS</p></td>
<td><p>设备关联服务</p></td>
</tr>
<tr class="even">
<td><p>前往</p></td>
<td><p>组所有者</p></td>
</tr>
<tr class="odd">
<td><p>PBC</p></td>
<td><p>按钮式连接</p></td>
</tr>
</tbody>
</table>

 

有关 Wi-Fi Direct 打印支持的常规信息所述[Wi-Fi Direct 打印概述](wfd-overview.md)。 请参阅[Wi-Fi Direct 打印实现](wfd-implementation.md)如何实现 Wi-Fi Direct 打印有关的详细信息。

## <a name="certification-requirements"></a>认证要求


没有新的认证要求是与此功能相关联。 请参阅**相关文档**下面，为适用的现有要求。

## <a name="hck-requirements"></a>HCK 要求


设备必须具有的 Wi-fi 联盟证书为 Wi-Fi Direct 实现。

打印设备的所有现有的证书要求包括需要跨所有可用的传输方式运行适用 HCK 测试应用。 合作伙伴应始终是指有任何更改的情况下发布的 Windows 认证团队的官方认证要求文档。

**请注意**  Wi-fi 联盟证书需求适用于 Wi-Fi Direct。 Wi-fi 联盟 Wi-Fi Direct 服务是单独的规范，并不支持在 Windows 中这一次。

 

## <a name="related-documents"></a>相关的文档


请参阅以下主题有关的相关信息：

[容器 Id 概述](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-container-ids)
[PnP x:Plug and Play for Windows 规范的扩展](https://msdn.microsoft.com/windows/hardware/gg463082)
[Wi-fi 联盟-Wi-Fi Direct 行业白皮书](https://go.microsoft.com/fwlink/p/?LinkId=784967)
 

 




