---
title: 视频微型端口驱动程序要求（Windows 2000 模型）
description: 视频微型端口驱动程序要求（Windows 2000 模型）
ms.assetid: f6ae5b71-97d5-4fd8-bd3d-7ee83f34581e
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1005c8addc4edde299a411126ed294b957ccb0b4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386111"
---
# <a name="video-miniport-driver-requirements-windows-2000-model"></a>视频微型端口驱动程序要求（Windows 2000 模型）


## <span id="ddk_video_miniport_driver_requirements_windows_2000_model__gg"></span><span id="DDK_VIDEO_MINIPORT_DRIVER_REQUIREMENTS_WINDOWS_2000_MODEL__GG"></span>


以下是一些微型端口驱动程序的要求。

-   **基于 NT 的操作系统微型端口驱动程序必须是单个** ***.sys*** **文件。**

    微型端口驱动程序包含单个二进制文件。 微型端口驱动程序的主要用途是检测、 初始化和配置一个或多个相同类型的图形适配器。

-   **微型端口驱动程序仅可导出的通话** ***videoprt.sys*。**

    微型端口驱动程序可以调用仅由系统提供的视频端口驱动程序导出这些函数。 (导出的视频端口函数列出引用页的后续[视频端口驱动程序函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。)驱动程序编写人员还可以使用以下确定微型端口驱动程序调用的函数：

    ```cpp
    link -dump -imports my_driver.sys
    ```

    微型端口驱动程序不能加载或使用未记录的操作系统函数调用的计算机上安装其他驱动程序。

-   **微型端口驱动程序可以启用平移收到最终用户的请求。**

    默认情况下，必须禁用平移。 仅当请求通过控件面板时，微型端口驱动程序应该启用它。 Oem 可以启用平移默认情况下为其预安装的一部分。

 

 





