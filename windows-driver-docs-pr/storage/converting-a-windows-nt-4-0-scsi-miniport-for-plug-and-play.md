---
title: 转换 Windows NT 4.0 SCSI 微型端口以实现即插即用
description: 转换 Windows NT 4.0 SCSI 微型端口以实现即插即用
ms.assetid: 46e5eb41-ff41-4054-856b-cc32f286e543
keywords:
- SCSI 微型端口驱动程序 WDK 存储，即插即用
- 即插即用 WDK SCSI
- Plug and Play WDK SCSI
- 转换 SCSI 微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7192f8e41bbef16bc8c0ec0d3a46fa4235327924
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330450"
---
# <a name="converting-a-windows-nt-40-scsi-miniport-for-plug-and-play"></a>转换 Windows NT 4.0 SCSI 微型端口以实现即插即用


## <span id="ddk_converting_a_windows_nt_4_0_scsi_miniport_for_plug_and_play_kg"></span><span id="DDK_CONVERTING_A_WINDOWS_NT_4_0_SCSI_MINIPORT_FOR_PLUG_AND_PLAY_KG"></span>


除非遵循特定的使用中的限制，否则即使微型端口驱动程序已启用插在注册表中，该驱动程序将错误在初始化期间*HwContext*指针和端口驱动程序提供的资源。 如果它依赖于驱动程序的可预测的初始化顺序的微型端口驱动程序可能还在初始化过程中出错。

若要在插即用，Microsoft Windows 下正常运行

NT 4.0 微型端口驱动程序的源代码可能需要修改以下各节中所述。

 

 




