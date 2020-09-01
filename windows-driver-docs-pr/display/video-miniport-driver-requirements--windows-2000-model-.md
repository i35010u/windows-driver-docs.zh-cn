---
title: 视频微型端口驱动程序要求（Windows 2000 模型）
description: 视频微型端口驱动程序要求（Windows 2000 模型）
ms.assetid: f6ae5b71-97d5-4fd8-bd3d-7ee83f34581e
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3771910256907c2ac2407fb766b7fa540114494e
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066302"
---
# <a name="video-miniport-driver-requirements-windows-2000-model"></a>视频微型端口驱动程序要求（Windows 2000 模型）


## <span id="ddk_video_miniport_driver_requirements_windows_2000_model__gg"></span><span id="DDK_VIDEO_MINIPORT_DRIVER_REQUIREMENTS_WINDOWS_2000_MODEL__GG"></span>


下面是视频微型端口驱动程序的一些要求。

-   **基于 NT 的操作系统视频微型端口驱动程序必须是单个** ***sys.databases*** **文件。**

    微型端口驱动程序由单个二进制文件组成。 微型端口驱动程序的主要用途是检测、初始化和配置同一类型的一个或多个图形适配器。

-   **小型小型驱动程序只能使调用导出**  ***videoprt.sys *。**

    微型端口驱动程序只能调用由系统提供的视频端口驱动程序导出的那些函数。  (导出的视频端口函数在 [视频端口驱动程序函数](/windows-hardware/drivers/ddi/index)后面的参考页面上列出。 ) 驱动程序编写者还可以使用以下内容来确定微型端口驱动程序调用的函数：

    ```cpp
    link -dump -imports my_driver.sys
    ```

    微型端口驱动程序无法使用未记录的操作系统函数调用在计算机上加载或安装其他驱动程序。

-   **小型小型驱动程序只能在收到最终用户请求时启用平移。**

    默认情况下，必须禁用平移。 只有通过控制面板请求微型端口驱动程序时，才应启用该驱动程序。 默认情况下，Oem 可以启用平移作为其预安装的一部分。

 

