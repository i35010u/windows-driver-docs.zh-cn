---
title: DirectX 文件版本号
description: DirectX 文件版本号
ms.assetid: 60f840d2-384c-49be-bf05-c16613b4858c
keywords:
- DirectX 文件版本数字 WDK 音频
- 版本编号 WDK 音频
- 音频的微型端口驱动程序 WDK，版本号
- 微型端口驱动程序 WDK 音频，版本号
- 音频驱动程序 WDK，版本号
- 驱动程序版本数字 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3172713d0d0435ec2d969e7f6cb3c704c09bccc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333767"
---
# <a name="directx-file-version-numbers"></a>DirectX 文件版本号


## <span id="directx_file_version_numbers"></span><span id="DIRECTX_FILE_VERSION_NUMBERS"></span>


支持 DirectX 的 Vxd 应满足的 DirectX 驱动程序版本号和驱动程序功能的安装程序要求。 请参阅 DirectX 8.0 程序员参考。 这些要求不适用于 WDM 或 Windows NT 4.0 驱动程序。

使用以下过程检查驱动程序版本号包括：

-   使用附带 DX 支持的任何游戏的安装程序应用程序安装设备驱动程序。 记录的所有已安装的文件，包括驱动程序安装包中的所有.drv、.dll、.vxd 和.exe 文件的版本号。

-   确认所有内部版本编号对应于外部 （字符串） 的版本号和数字遵循版本编号的规则 (请参阅[音频驱动程序的版本号](version-numbers-for-audio-drivers.md))。

-   使用 Windows 资源管理器查看包含文件的目录。 右键单击每个文件，然后单击**属性**以验证的版权信息是否正确。 具体而言，验证供应商名称为您的驱动程序未指定"Microsoft"。

 

 




