---
title: 设置文件信息处理
description: 设置文件信息处理
ms.assetid: bda94e8d-0be1-4730-a82e-4aa4d3763cce
keywords:
- 安全 WDK 文件系统，语义模型检查
- 语义模型检查 WDK 文件系统，设置文件信息处理
- 设置文件信息处理 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ac7afc3c1c10d25b2cac3e6938dc37ecef1f950
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89062998"
---
# <a name="set-file-information-processing"></a>设置文件信息处理


## <span id="ddk_set_file_information_processing_if"></span><span id="DDK_SET_FILE_INFORMATION_PROCESSING_IF"></span>


I/o 管理器对 [**IRP \_ MJ \_ 集 \_ 信息**](./irp-mj-set-information.md)支持的信息类的子集执行一些额外检查。 具体而言，对于 FileRenameInformation、FileLinkInformation 和 FileMoveClusterInformation，i/o 管理器向目标名称的父目录发出一个打开的，以确保用户在将 IRP \_ MJ \_ 集 \_ 信息请求发送到文件系统之前有权在该父目录下创建一个子节点。

 

