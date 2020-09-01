---
title: POS 事件
description: 使用 ReadFile 描述从设备驱动程序传递到服务 (POS) API 层的点的事件。
ms.assetid: 1123b789-c0ee-4490-9081-79c08fc31417
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 88b7194ec09f6bd297f85a6ae432906719bbbb58
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189767"
---
# <a name="pos-events"></a>POS 事件

本部分介绍使用 [ReadFile](/windows/desktop/api/fileapi/nf-fileapi-readfile)从设备驱动程序传递到服务 (POS) API 层的事件。 当应用程序通过 POS API 成功声明设备时，运行时将对设备驱动程序进行持续读取操作以接收事件。 I/o 基于消息。 **ReadFile** 需要传入足够大的缓冲区，才能读取当前事件。 驱动程序将保留消息，直到具有足够的输出缓冲区的读取请求读取整个消息。

## <a name="in-this-section"></a>本节内容

[ReleaseDeviceRequested](releasedevicerequested.md)

[StatusUpdated](statusupdated.md)