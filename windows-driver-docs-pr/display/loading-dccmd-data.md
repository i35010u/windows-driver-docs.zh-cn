---
title: 加载 DCCMD 数据
description: 加载 DCCMD 数据
ms.assetid: 2fceaaa6-5604-4130-ae33-8567561fcccb
keywords:
- alpha 混合数据加载 WDK DirectX VA
- 混合型的图片 WDK DirectX VA，alpha 混合数据加载
- DCCMD WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb5046a3911ec69a3b954193aaae8332c3beb5cb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347567"
---
# <a name="loading-dccmd-data"></a>加载 DCCMD 数据


## <span id="ddk_loading_dccmd_data_gg"></span><span id="DDK_LOADING_DCCMD_DATA_GG"></span>


DCCMD （显示控制命令） 数据的格式与 DVD ROM 规范兼容的方式，并且将以及突出显示的数据应用到 DPXD 面以创建一个 alpha 值混合处理的图面。 DCCMD 数据缓冲区的内容必须包含一系列 DVD DCCMDs 格式的数据。 DVD 子画面定义和数据字段的解释的进一步说明，请参阅*DVD 规范为只读磁盘：第 3 部分-视频规范 （版本 1.11，1999 年 5）*。

 

 





