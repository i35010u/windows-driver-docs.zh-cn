---
title: Windows XP 和 Windows Me 的 WIA 底片扫描仪兼容性
description: Windows XP 和 Windows Me 的 WIA 底片扫描仪兼容性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d161a5414789c8bca2611a7c9baa9f15c066ed52
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820227"
---
# <a name="wia-film-scanner-compatibility-for-windows-xp-and-windows-me"></a>Windows XP 和 Windows Me 的 WIA 底片扫描仪兼容性





对于 Microsoft Windows XP 或 Windows Me，胶片扫描项 *不* 存在。 胶片扫描器 (专用胶片扫描器或平板扫描仪上的胶卷扫描器附件) 将不能用于在 Windows Vista 上运行的 Windows XP WIA 应用程序。 在 windows Vista WIA 服务中找到的 [Wia 兼容层](wia-compatibility-layer.md) 仅处理适用于 windows \_ \_ \_ \_ XP 应用 \_ \_ \_ \_ \_)  (程序的平板和基本送纸器项 (适用于 WINDOWS vista 设备的 "wia" 类别平板和 "wia" 类别送) 料

如果实现了一个平台项来模拟胶卷项的基本功能，则可以为运行 Windows Vista 的 Windows XP WIA 应用程序提供基本支持。 显示给用户的默认用户界面将与平板扫描仪相同，因此应用程序只接收单个帧。 而且，即使使用此类平板，Windows Vista 驱动程序也不能在 Windows XP 上运行，因为它仅对 Windows Vista 上的 Windows XP 应用程序提供有限的支持。

**注意**   如果扫描仪还支持平板扫描，则 WIA 平板扫描仪项必须是 "扫描仪" 项树中的第一个 WIA 子项目。

 

有关 Windows XP 和 Windows Me 兼容性的详细信息，请参阅 [Windows me 和 WINDOWS XP 的 WIA 平板扫描仪兼容性](wia-flatbed-scanner-compatibility-for-windows-xp-and-windows-me.md)。

 

 




