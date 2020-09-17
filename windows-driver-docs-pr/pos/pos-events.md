---
title: POS 事件
description: 使用 ReadFile 描述从设备驱动程序传递到服务 (POS) API 层的点的事件。
ms.assetid: 1123b789-c0ee-4490-9081-79c08fc31417
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3ee4b7a8a1844a13cf87ccfa06ccf278eef85a5c
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90714866"
---
# <a name="pos-events"></a>POS 事件

本部分介绍使用 [ReadFile](/windows/win32/api/fileapi/nf-fileapi-readfile)从设备驱动程序传递到服务 (POS) API 层的事件。 当应用程序通过 POS API 成功声明设备时，运行时将对设备驱动程序进行持续读取操作以接收事件。 I/o 基于消息。 **ReadFile** 需要传入足够大的缓冲区，才能读取当前事件。 驱动程序将保留消息，直到具有足够的输出缓冲区的读取请求读取整个消息。

## <a name="in-this-section"></a>在本节中

[ReleaseDeviceRequested](releasedevicerequested.md)

[StatusUpdated](statusupdated.md)