---
title: 视频微型端口驱动程序标头文件（Windows 2000 模型）
description: 视频微型端口驱动程序标头文件（Windows 2000 模型）
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，头文件
- 标头文件 WDK 视频微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f1bf50b7e4facc1a7a9682fee0b0eaff0419470
ms.sourcegitcommit: abd90176b0416a1170b1c0232943b60543dd6b98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/29/2020
ms.locfileid: "97812493"
---
# <a name="video-miniport-driver-header-files-windows-2000-model"></a>视频微型端口驱动程序标头文件（Windows 2000 模型）

Windows 2000 显示器驱动程序模型中的视频微型端口驱动程序包括以下头文件：

| 文件名 | 目录 |
| --------- | -------- |
| *dderror* | 包含微型端口驱动程序返回到视频端口驱动程序的 Win32 状态常量，该驱动程序也返回到微型端口驱动程序的对应内核模式显示驱动程序。 |
| *devioctl* | 包含用于定义 i/o 控制代码的宏和常量。 |
| *小型端口。h* | 包含用于视频 (和 SCSI) 微型端口驱动程序的基本类型、常量和结构。 |
| *ntddvdeo* | 包含系统定义的 i/o 控制代码 (IOCTLs) 和 (VRPs) 视频微型端口驱动程序的视频请求数据包中发送的相应结构。 |
| *tvout* | 包含用于实现电视连接器和副本保护支持以及此结构中使用的常量的 **VIDEOPARAMETERS** 结构。 |
| *视频。h* | 包含 **VideoPort**_Xxx_ 和 *SvgaHwIoPortXxx* 视频端口函数声明、特定于视频的结构，如 **VIDEO_REQUEST_PACKET** 和 *HwVidXxx* 视频微型端口函数原型。 |
| *videoagp* | 包含 AGP 特定的结构、 *AgpXxx* 微型端口驱动程序函数原型，以及在视频微型端口驱动程序中实现 AGP 支持所需的 **VideoPort**_Xxx_ 函数声明。 |

这些标头附带了 Windows 驱动程序工具包 (WDK) 。 有关这些头文件中的函数、结构、系统定义的 i/o 控制代码和常量的详细信息，请参阅 [使用图形 DDI](using-the-graphics-ddi.md)。
