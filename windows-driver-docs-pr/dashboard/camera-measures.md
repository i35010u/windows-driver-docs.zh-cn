---
title: 相机度量
description: 相机度量在蓝牙驱动程序外部测试过程中筛选出良性初始化错误
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: e8c8604113d5c500bed65d2a4a2685ed147b4043
ms.sourcegitcommit: f8619f20a0903dd64f8641a5266ecad6df5f1d57
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91423788"
---
# <a name="camera-measures"></a>相机度量

## <a name="description"></a>说明

在 Windows 10 中，Microsoft 提供[通用照相机驱动程序设计指南](../stream/windows-10-technical-preview-camera-drivers-design-guide.md)，其中讨论了相机驱动程序接口如何支持所有与相机相关的设备。 该模型包含新的 DDI，例如数字视频稳定、可变帧速率、人脸检测以及许多其他功能。 通用相机驱动程序是一种在 Windows 驱动模型上构建的 AVStream 微型驱动器；AVStream 是 Microsoft 提供的多媒体类驱动程序，支持仅视频流式处理和集成的视频和音频流式处理。 有关 AVStream 的详细信息，请参阅 [AVStream 微型驱动程序设计指南](../stream/avstream-minidrivers-design-guide.md)。
