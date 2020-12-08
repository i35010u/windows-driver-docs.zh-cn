---
title: 通过可移动设备功能生成的容器 ID
description: 通过可移动设备功能生成的容器 ID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 231924f06a38f5837f3b27949da073fcc73014ff
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782943"
---
# <a name="container-ids-generated-from-the-removable-device-capability"></a>通过可移动设备功能生成的容器 ID


从 Windows 7 开始，如果总线驱动程序无法为设备 *节点 (的* 容器 id 提供枚举的) ，则即插即用 (PnP) manager 使用可移动设备功能为该物理设备的所有 devnodes 枚举生成容器 id。 总线驱动程序报告可移动设备的功能，以响应 [**IRP_MN_QUERY_CAPABILITIES**](../kernel/irp-mn-query-capabilities.md) 的请求。

本节包含下列主题：

[可移动设备功能概述](overview-of-the-removable-device-capability.md)

[如何通过可移动设备功能生成容器 ID](how-container-ids-are-generated-from-the-removable-device-capability.md)

 

