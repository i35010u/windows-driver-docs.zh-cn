---
title: POS 事件
description: 使用 ReadFile 描述从设备驱动程序传递到服务 (POS) API 层的点的事件。
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: cf9c93b29acaba675edd6d127cfb57cad73a4abd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794307"
---
# <a name="pos-events"></a>POS 事件

本部分介绍使用 [ReadFile](/windows/win32/api/fileapi/nf-fileapi-readfile)从设备驱动程序传递到服务 (POS) API 层的事件。 当应用程序通过 POS API 成功声明设备时，运行时将对设备驱动程序进行持续读取操作以接收事件。 I/o 基于消息。 **ReadFile** 需要传入足够大的缓冲区，才能读取当前事件。 驱动程序将保留消息，直到具有足够的输出缓冲区的读取请求读取整个消息。

## <a name="in-this-section"></a>在本节中

[ReleaseDeviceRequested](releasedevicerequested.md)

[StatusUpdated](statusupdated.md)
