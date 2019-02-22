---
title: 单一驱动程序为 Windows Vista 和 Windows XP
description: 单一驱动程序为 Windows Vista 和 Windows XP
ms.assetid: 3fa9c044-ab9d-4bed-b5fc-89396e1269ce
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3edbdf8a89adf63f0270e561755597c2d1ceb724
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545500"
---
# <a name="single-driver-for-windows-vista-and-windows-xp"></a>单一驱动程序为 Windows Vista 和 Windows XP


您可能想要为 Windows Vista 和 Windows XP 单个驱动程序。 在这种情况下，该驱动程序通过检查标志来处理数据传输。 当[ **IWiaMiniDrv::drvAcquireItemData** ](https://msdn.microsoft.com/library/windows/hardware/ff543956)称为基于流的传输*lFlags*参数设置为任一 WIA\_MINIDRV\_传输\_下载或 WIA\_MINIDRV\_传输\_上传。 如果这些位未设置，则传输*旧*传输和驱动程序应遵循的 Windows XP 数据传输所述的行为。

 

 




