---
title: 视频微型端口驱动程序要求（Windows 2000 模型）
description: 视频微型端口驱动程序要求（Windows 2000 模型）
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdd76df5aad286e3ec620916e40b36de8da81b5c
ms.sourcegitcommit: abd90176b0416a1170b1c0232943b60543dd6b98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/29/2020
ms.locfileid: "97812491"
---
# <a name="video-miniport-driver-requirements-windows-2000-model"></a>视频微型端口驱动程序要求（Windows 2000 模型）

下面是视频微型端口驱动程序的一些要求。

* 基于 NT 的操作系统视频微型端口驱动程序必须是单个 *sys.databases* 文件。

  微型端口驱动程序由单个二进制文件组成。 微型端口驱动程序的主要用途是检测、初始化和配置同一类型的一个或多个图形适配器。

* 微型端口驱动程序只能使调用 *videoprt.sys* 导出。

  微型端口驱动程序只能调用由系统提供的视频端口驱动程序导出的那些函数。  驱动程序编写器还可以使用以下操作来确定微型端口驱动程序调用的函数：

    ```cpp
    link -dump -imports my_driver.sys
    ```

    微型端口驱动程序无法使用未记录的操作系统函数调用在计算机上加载或安装其他驱动程序。

* 小型小型驱动程序只能在收到最终用户请求时启用平移。

  默认情况下，必须禁用平移。 只有通过控制面板请求微型端口驱动程序时，才应启用该驱动程序。 默认情况下，Oem 可以启用平移作为其预安装的一部分。
