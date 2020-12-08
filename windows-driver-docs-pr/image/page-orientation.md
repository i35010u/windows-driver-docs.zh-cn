---
title: 页面方向
description: 页面方向
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 028a014b3fe9dfccabb2d85e783279ec5a7a045b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841095"
---
# <a name="page-orientation"></a>页面方向


WIA 微型驱动程序必须确保 WIA \_ IPS \_ 方向属性与当前的选择区域一致。 如果应用程序将 WIA ips 方向的值更改 \_ \_ 为对当前选定页面大小无效的方向，则微型驱动程序应将 "wia ip 页面大小" 的值更改 \_ \_ \_ 为新方向值所支持的页面大小。

请注意，如果 [**WIA \_ ip \_ 方向**](./wia-ips-orientation.md) 设置为 LANSCAPE，则区设置将为 "翻转"。 例如，如果应用程序将 WIA \_ ip \_ 页面大小设置 \_ 为 wia \_ 页面 \_ A4，则微型驱动程序应将 [**wia \_ ip \_ 页面 \_ 宽度**](./wia-ips-page-width.md) 设置为11692，将 [**wia \_ ip \_ 页面 \_ 高度**](./wia-ips-page-height.md) 设置为8267。  (微型驱动程序还应相应地设置 [**WIA \_ ip \_ XEXTENT**](./wia-ips-xextent.md) 和 [**Wia \_ ip \_ YEXTENT**](./wia-ips-yextent.md) 。 ) 请注意，如果 wia \_ ip \_ 页面 \_ 大小设置为 wia \_ 页面 \_ 自定义，则不会使用方向设置来确定要扫描的页面的范围维度。

 

