---
title: 页面大小和方向
description: 页面大小和方向
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f739c27f78c28696f8a1fb76ffa4642300b5f42f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841091"
---
# <a name="page-size-and-orientation"></a>页面大小和方向


页面大小和方向的扫描程序设置是相互关联的。 两者均可确定要扫描的页面的大小。

例如，WIA 属性列表使用的页大小和范围值 \_ \_ 取决于 "wia ip 方向" 属性的有效设置 \_ \_ 。 因此，如果设备无法使用 WIA 页面 A4 设置扫描面向横向的 \_ 文档 \_ ， \_ \_ \_ \_ \_ 当 wia \_ ip \_ 方向设置为 LANSCAPE 时，wia 页 a4 不应出现在 "wia ip 页面大小" 属性的有效值列表中。

" [**WIA \_ IPS \_ 方向**](./wia-ips-orientation.md) " 属性的值确定当前所选页面的方向。 " [**Wia \_ ip \_ 页面 \_ 高度**](./wia-ips-page-height.md) " 和 " [**wia \_ ip \_ 页面 \_ 宽度**](./wia-ips-page-width.md) " 属性报告页面的尺寸，以英寸的分之几分之)  (。 这些 height 和 width 属性必须包含与 [**wia \_ ips \_ XEXTENT**](./wia-ips-xextent.md) 和 [**wia \_ ips \_ YEXTENT**](./wia-ips-yextent.md)中的值等效的值，这些值提供以像素为单位的页面尺寸。

有关使用页面大小和方向的详细信息，请参阅以下主题：

[支持的扫描仪纸张大小](supported-scanner-paper-sizes.md)

[自定义的和自动设置的页面大小](custom-and-auto-page-sizes.md)

[页面方向](page-orientation.md)

[扫描仪页面大小和方向代码示例](page-size-and-orientation-code-examples.md)

 

