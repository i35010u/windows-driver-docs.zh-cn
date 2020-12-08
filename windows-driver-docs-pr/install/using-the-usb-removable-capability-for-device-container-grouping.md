---
title: 将 USB 可移动功能用于设备容器分组
description: 将 USB 可移动功能用于设备容器分组
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a2cccf3d150438a2f90a22bd452d69a71b64de5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840953"
---
# <a name="using-the-usb-removable-capability-for-device-container-grouping"></a>将 USB 可移动功能用于设备容器分组


USB **可移动** 功能允许操作系统为旧设备创建设备容器。 此机制可为无法提供 Microsoft 操作系统 **ContainerID** 描述符的设备提供向后兼容性，或与不具有 usb 端口功能的计算机集成的设备的向后兼容性 (**_UPC** 相应 usb 端口) 值。

必须认识到，USB 集线器驱动程序使用物理 USB 硬件中的可用 removability 信息，以便报告连接到其内部或外部端口的设备的更准确的 **可移动** 功能。 有关详细信息，请参阅 [从可移动设备功能生成的容器 id](container-ids-generated-from-the-removable-device-capability.md)。

 

 





