---
title: POS 事件
description: 介绍从传递的设备驱动程序到点的服务 (POS) API 层通过 ReadFile 的事件。
ms.assetid: 1123b789-c0ee-4490-9081-79c08fc31417
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 629658ba43349510468469b837a4d8a4a6d9bf7f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564220"
---
# <a name="pos-events"></a>POS 事件

本部分介绍从设备驱动程序到点的服务 (POS) API 层通过使用传递的事件[ReadFile](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)。 当应用程序已成功对声明设备通过 POS API 时，运行时将维护针对设备驱动程序以接收事件的连续读的操作。 I/O 是基于消息的。 **ReadFile**需将传入的缓冲区不够大，足以无法读取当前事件中。 该驱动程序直到与足够的输出缓冲区的读取请求读取整个消息由保留该消息。

## <a name="in-this-section"></a>本节内容

[ReleaseDeviceRequested](releasedevicerequested.md)

[StatusUpdated](statusupdated.md)
