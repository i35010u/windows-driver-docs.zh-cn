---
title: 加载 DCCMD 数据
description: 加载 DCCMD 数据
keywords:
- alpha-blend 数据加载 WDK DirectX VA
- 混合图片 WDK DirectX VA，alpha-blend 数据加载
- DCCMD WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4390f8f931bfb6cafe31b4840dadb2c27b26e76c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796255"
---
# <a name="loading-dccmd-data"></a>加载 DCCMD 数据


## <span id="ddk_loading_dccmd_data_gg"></span><span id="DDK_LOADING_DCCMD_DATA_GG"></span>


DCCMD (显示控件命令) 数据的格式设置方式与 DVD ROM 规范兼容，并将与突出显示数据一起应用于 DPXD 图面，以创建 alpha 混合图面。 DCCMD 数据缓冲区内容必须包含格式为 DVD DCCMDs 列表的数据。 有关 DVD 子画面定义和数据字段解释的详细说明，请参阅 *Read-Only 磁盘的 DVD 规范：第3部分-视频规范 (版本1.11，) 1999*。

 

 





