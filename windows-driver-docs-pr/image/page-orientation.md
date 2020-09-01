---
title: 页面方向
description: 页面方向
ms.assetid: fb28863a-920a-4b26-a652-fb255622824f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 509cfff640f400cdbc474fb3fa447a4020f28a32
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192603"
---
# <a name="page-orientation"></a>页面方向


WIA 微型驱动程序必须确保 WIA \_ IPS \_ 方向属性与当前的选择区域一致。 如果应用程序将 WIA ips 方向的值更改 \_ \_ 为对当前选定页面大小无效的方向，则微型驱动程序应将 "wia ip 页面大小" 的值更改 \_ \_ \_ 为新方向值所支持的页面大小。

请注意，如果 [**WIA \_ ip \_ 方向**](./wia-ips-orientation.md) 设置为 LANSCAPE，则区设置将为 "翻转"。 例如，如果应用程序将 WIA \_ ip \_ 页面大小设置 \_ 为 wia \_ 页面 \_ A4，则微型驱动程序应将 [**wia \_ ip \_ 页面 \_ 宽度**](./wia-ips-page-width.md) 设置为11692，将 [**wia \_ ip \_ 页面 \_ 高度**](./wia-ips-page-height.md) 设置为8267。  (微型驱动程序还应相应地设置 [**WIA \_ ip \_ XEXTENT**](./wia-ips-xextent.md) 和 [**Wia \_ ip \_ YEXTENT**](./wia-ips-yextent.md) 。 ) 请注意，如果 wia \_ ip \_ 页面 \_ 大小设置为 wia \_ 页面 \_ 自定义，则不会使用方向设置来确定要扫描的页面的范围维度。

 

