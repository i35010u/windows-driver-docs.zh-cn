---
title: Pscript 支持的转义符
description: Pscript 支持的转义符
keywords:
- PostScript 打印机驱动程序 WDK 打印，转义
- Pscript WDK 打印，转义
- 转义 WDK Pscript
ms.date: 03/28/2021
ms.localizationpriority: medium
ms.openlocfilehash: feeb62f83526958cab9c9b78067959f97b648e3b
ms.sourcegitcommit: 7518452c415b32d8c97da3cbc5f39725ae619b5e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2021
ms.locfileid: "105719045"
---
# <a name="pscript-supported-escapes"></a>Pscript 支持的转义符

Pscript5 打印机驱动程序支持以下转义。

| Escape | 说明 |
|--|--|
| BEGIN_PATH | 打开路径。 |
| CHECKJPEGFORMAT | 确定打印机是否可以处理 JPEG 图像。 有关此转义的详细信息，请参阅 [CHECKJPEGFORMAT](/previous-versions/windows/desktop/legacy/dd183421(v=vs.85))。<br><br>此转义将生成对 [DrvQueryDeviceSupport](/windows/win32/api/winddi/nf-winddi-drvquerydevicesupport) 函数的调用。 |
| CHECKPNGFORMAT | 确定打印机是否可以处理 PNG 图像。 有关此转义的详细信息，请参阅 [CHECKPNGFORMAT](/previous-versions/windows/desktop/legacy/dd183424(v=vs.85))。<br><br>此转义将生成对 [DrvQueryDeviceSupport](/windows/win32/api/winddi/nf-winddi-drvquerydevicesupport) 函数的调用。 |
| CLIP_TO_PATH | 定义按路径绑定的剪辑区域。 |
| DOWNLOADHEADER | 下载所有 procsets (，即 PostScript 过程) 集。 |
| DRAWPATTERNRECT | 通过使用页面控件语言的模式和规则功能 (PCL) 在 Hewlett Packard LaserJet 或 LaserJet 兼容的打印机上，创建一个白色、灰度或实心黑色矩形。 灰度是一种灰色模式，其中包含黑色和白色像素的特定混合。 有关此转义的详细信息，请参阅 [DRAWPATTERNRECT](/previous-versions/windows/desktop/legacy/dd162495(v=vs.85))。<br><br>此 escape 与驱动程序的 [DrvEscape](/windows/win32/api/winddi/nf-winddi-drvescape) 函数相关联。 |
| ENCAPSULATED_POSTSCRIPT | 将封装的 PostScript (EPS) 数据发送到打印机。<br><br>此 escape 与驱动程序的 [DrvDrawEscape](/windows/win32/api/winddi/nf-winddi-drvdrawescape) 函数相关联。 |
| END_PATH | 结束路径。 |
| EPSPRINTING | 指示 EPS 打印的开始或结束。<br><br>图形设备接口 (GDI) 会截获此转义，并将其转换为非 DrvEscape 的 DDI 调用。 打印机驱动程序未收到此转义符。 |
| GET_PS_FEATURESETTING | 获取有关 PostScript 驱动程序的指定功能设置的信息。<br><br>有关此转义的详细信息，请参阅 [GET_PS_FEATURESETTING](/previous-versions/windows/desktop/legacy/dd144954(v=vs.85))。 |
| GETTECHNOLOGY | 获取打印机的常规技术类型。 Windows 3.0 之后为 Windows 操作系统版本编写的打印机驱动程序可能不支持此转义。 |
| 直通 | 将数据直接发送到兼容模式或以 GDI 为中心的模式下的 PostScript 打印机驱动程序。 Postscript 模式下的 PostScript 打印机驱动程序不支持此转义。<br><br>有关此转义的详细信息，请参阅 [PASSTHROUGH](/previous-versions/windows/desktop/legacy/dd162776(v=vs.85))。 |
| POSTSCRIPT_DATA | 直接将数据发送到打印机驱动程序。 此转义与传递转义完全相同，只是 PostScript 打印机驱动程序仅支持 Windows NT 4.0 兼容模式下的此转义。<br><br>有关此转义的详细信息，请参阅 [POSTSCRIPT_DATA](/previous-versions/windows/desktop/legacy/dd162828(v=vs.85))。 |
| POSTSCRIPT_IDENTIFY | 将 PostScript 打印机驱动程序设置为以 GDI 为中心或以 PostScript 模式。<br><br>有关此转义的详细信息，请参阅 [POSTSCRIPT_IDENTIFY](/previous-versions/windows/desktop/legacy/dd162829(v=vs.85))。 |
| POSTSCRIPT_IGNORE | 取消输出。<br><br> |
| POSTSCRIPT_INJECTION | 在 PostScript 作业流中插入原始数据块。<br><br> |
| POSTSCRIPT_PASSTHROUGH | 在 Windows NT 4.0 兼容性模式或以 PostScript 模式模式下直接将数据发送到 PostScript 打印机驱动程序。 以 GDI 为中心的模式中的 PostScript 打印机驱动程序不支持此转义。<br><br> |
| QUERYESCSUPPORT | 确定设备驱动程序是否实现了特定的转义。<br><br> |
| SETCOPYCOUNT | 设置要打印的份数。<br><br>此 escape 已由 [DocumentProperties](/windows/win32/printdocs/documentproperties) 和 [PrinterProperties](/windows/win32/printdocs/printerproperties) 函数取代。 |
| SPCLPASSTHROUGH2 | 使应用程序能够将私有过程和其他资源包含在文档级别-保存上下文中。<br><br>有关此转义的详细信息，请参阅 [SPCLPASSTHROUGH2](/previous-versions/windows/desktop/legacy/dd145110(v=vs.85))。 |
