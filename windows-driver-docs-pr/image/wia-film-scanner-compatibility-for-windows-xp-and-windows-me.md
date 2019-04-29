---
title: Windows XP 和 Windows Me 的 WIA 底片扫描仪兼容性
description: Windows XP 和 Windows Me 的 WIA 底片扫描仪兼容性
ms.assetid: 9f96ef72-2482-435f-b512-b48c12dc1628
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 427f4e8d5a222bb24e9b536d245a0c7e5e6c3f26
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360334"
---
# <a name="wia-film-scanner-compatibility-for-windows-xp-and-windows-me"></a>Windows XP 和 Windows Me 的 WIA 底片扫描仪兼容性





执行的扫描项目的电影胶片*不*存在的 Microsoft Windows XP 或 Windows me 一起提供。 电影扫描仪 （专用的电影扫描程序或平板扫描仪上的电影胶片扫描程序附件） 将不能在 Windows Vista 运行的 Windows XP WIA 应用程序。 [WIA 兼容性层](wia-compatibility-layer.md)位于 Windows Vista WIA 服务句柄仅平板和基本的送纸器项 (WIA\_类别\_平板和 WIA\_类别\_送纸器) 适用于 Windows Vista 设备时用于 Windows XP 应用程序;电影和存储的项 (WIA\_类别\_电影和 WIA\_类别\_已完成\_文件) 不会翻译。

您可以运行 Windows Vista，如果你实现了平板项，以模拟电影项的基本功能的 Windows XP WIA 应用程序提供基本支持。 向用户显示的默认用户界面会相同平板扫描仪，请使该应用程序将只会收到单个帧。 而，即使使用此类平板项，Windows Vista 驱动程序将无法工作在 Windows XP 上因为它为 Windows Vista 上的 Windows XP 应用程序提供有限的支持。

**请注意**  扫描仪还支持平板扫描，如果 WIA 平板扫描仪项必须是扫描程序项树中的第一个 WIA 子项目。

 

有关 Windows XP 和 Windows Me 兼容性的详细信息，请参阅[WIA 平板扫描仪兼容性的 Windows Me 和 Windows XP](wia-flatbed-scanner-compatibility-for-windows-xp-and-windows-me.md)。

 

 




