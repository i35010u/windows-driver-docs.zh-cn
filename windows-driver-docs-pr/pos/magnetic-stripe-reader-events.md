---
title: 磁条读取器事件
description: 介绍从传递的设备驱动程序到点的服务 (POS) API 层通过 ReadFile 的事件。
ms.assetid: 48ce9fcb-5ea2-4045-92df-990d94e5e98b
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: b8f45fcc9c7be37d37a14ba84755d3dee8bb82a5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349312"
---
# <a name="magnetic-stripe-reader-events"></a>磁条读取器事件

本部分介绍从设备驱动程序到点的服务 (POS) API 层通过使用传递的事件[ReadFile](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)。 本部分重点介绍特定于磁条阅读器 (MSRs) 的事件。

## <a name="in-this-section"></a>本节内容

[MagneticStripeReaderDataReceived](magneticstripereaderdatareceived.md)  
在成功扫描事件后发生。

[MagneticStripeReaderErrorOccured](magneticstripereadererroroccured.md)  
当 MSR 错误，例如扫描错误时发生。
