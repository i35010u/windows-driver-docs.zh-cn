---
title: 设置文件信息处理
description: 设置文件信息处理
ms.assetid: bda94e8d-0be1-4730-a82e-4aa4d3763cce
keywords:
- 安全 WDK 文件系统，语义模型检查
- 语义模型检查 WDK 的文件系统中，设置文件的信息处理
- 设置处理 WDK 文件系统的文件信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3cd1768adedd72e6df380902de5bfa3ca975c6e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344443"
---
# <a name="set-file-information-processing"></a>设置文件信息处理


## <span id="ddk_set_file_information_processing_if"></span><span id="DDK_SET_FILE_INFORMATION_PROCESSING_IF"></span>


I/O 管理器执行一些额外的检查的支持的信息类子集[ **IRP\_MJ\_设置\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff549366)。 具体而言，FileRenameInformation、 FileLinkInformation 和 FileMoveClusterInformation，I/O 管理器发出一个打开的父目录的目标名称，以确保用户具有访问权限之前向下发送创建该父级下的子级IRP\_MJ\_设置\_到文件系统的信息请求。

 

 




