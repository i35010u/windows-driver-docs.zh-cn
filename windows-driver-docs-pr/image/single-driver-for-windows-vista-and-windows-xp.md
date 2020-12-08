---
title: 用于 Windows Vista 和 Windows XP 的单一驱动程序
description: 用于 Windows Vista 和 Windows XP 的单一驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35dc068001e43de0f72ff7e9aef16530e903202f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802445"
---
# <a name="single-driver-for-windows-vista-and-windows-xp"></a>用于 Windows Vista 和 Windows XP 的单一驱动程序


你可能希望为 Windows Vista 和 Windows XP 使用单个驱动程序。 在这种情况下，驱动程序通过检查标志来处理数据传输。 当 [**IWiaMiniDrv：**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata) 对基于流的传输调用:d rvacquireitemdata 时， *lFlags* 参数设置为 WIA \_ MINIDRV \_ 传输 \_ 下载或 wia \_ MINIDRV \_ 传输 \_ 上传。 如果这两个位均未设置，则表示传输为 *传统* 传输，驱动程序应遵循 Windows XP 数据传输中所述的行为。

 

