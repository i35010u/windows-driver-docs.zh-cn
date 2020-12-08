---
title: DirectX 文件版本号
description: DirectX 文件版本号
keywords:
- DirectX 文件版本号 WDK 音频
- 版本号 WDK 音频
- 音频微型端口驱动程序 WDK，版本号
- 微型端口驱动程序 WDK 音频，版本号
- 音频驱动程序 WDK，版本号
- 驱动程序版本号 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6c418ea5869d73b8c7807bca3cecb276e630ac8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786591"
---
# <a name="directx-file-version-numbers"></a>DirectX 文件版本号


## <span id="directx_file_version_numbers"></span><span id="DIRECTX_FILE_VERSION_NUMBERS"></span>


支持 DirectX 的 Vxd 应满足驱动程序版本号和驱动程序功能的 DirectX 设置要求。 请参阅 DirectX 8.0 程序员参考。 这些要求不适用于 WDM 或 Windows NT 4.0 驱动程序。

使用以下过程检查驱动程序版本号：

-   使用与支持 DX 的任何游戏一起提供的安装应用程序来安装设备驱动程序。 记录所有已安装文件的版本号，包括驱动程序安装包中的所有 winspool.drv、.dll、.vxd 和 .exe 文件。

-   确认所有内部版本号都对应于外部 (字符串) 版本号，并且数字遵循了版本编号规则 (请参阅 [音频驱动程序) 版本号](version-numbers-for-audio-drivers.md) 。

-   使用 Windows 资源管理器查看包含这些文件的目录。 右键单击每个文件，然后单击 " **属性** " 以验证版权信息是否正确。 具体而言，验证驱动程序是否未将 "Microsoft" 指定为供应商名称。

 

 




