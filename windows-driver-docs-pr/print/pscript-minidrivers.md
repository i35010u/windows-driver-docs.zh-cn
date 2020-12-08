---
title: Pscript 微型驱动程序
description: Pscript 微型驱动程序
keywords:
- PostScript 打印机驱动程序 WDK 打印，微型驱动程序
- Pscript WDK 打印，微型驱动程序
- 微型驱动程序 WDK Pscript
- 微型驱动程序 WDK Pscript，关于 Pscript 微型驱动程序
- PPD 文件 WDK 打印
- ppd 文件
- CONTOSO.NTF 文件
- contoso.ntf 文件
- 东亚字体 WDK 打印
- 亚洲字体 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bc55da9128c51879de0bb7caffe10fae40b356f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807157"
---
# <a name="pscript-minidrivers"></a>Pscript 微型驱动程序





Pscript 微型驱动程序是从 ppd 文件和 contoso.ntf 文件创建的。

### <a name="ppd-files"></a><a href="" id="ddk-ppd-files-gg"></a>PPD 文件

基于文本的 PostScript 打印机说明文件 ( ppd 文件) 说明 PostScript 打印机的特征。 适用于 Microsoft Windows 2000 和更高版本的 Pscript 驱动程序支持与 Adobe Systems，Inc. 的 PPD 规范版本4.3 兼容的 ppd 文件，并将文本转换为二进制格式，该格式在本地存储为 bpd 文件，该文件在每次更改时重新生成。

### <a name="ntf-files"></a><a href="" id="ddk-ntf-files-gg"></a>CONTOSO.NTF 文件

Windows 2000 和更高版本的字体文件 ( contoso.ntf 文件) 是二进制文件，用于描述 Pscript 支持的打印机的设备字体。

Microsoft 提供名为 pscript. contoso.ntf 的 contoso.ntf 文件，其中包含常见的美国设备字体的描述。 对于中文打印机，Microsoft 还提供了一个名为 pscrptfe contoso.ntf 的 contoso.ntf 文件，其中包含经常遇到的东亚设备字体的描述。

此外，硬件供应商还可以为 pscript 不支持的字体提供设备字体说明。 可以通过将 [AFM 文件转换为 contoso.ntf 文件来](converting-afm-files-to-ntf-files.md)创建这些字体说明。 自定义打印机型号特定的 contoso.ntf 文件可以通过在 [打印机 INF 文件](printer-inf-files.md)中将其作为依赖文件列出来安装。 有关详细信息，请参阅 [安装 Pscript 微型驱动程序](installing-a-pscript-minidriver.md)。

Pscript 通过先检查打印机型号特定的 contoso.ntf 文件，然后检查 Pscript，并使用找到的第一个字体说明，搜索字体指标。

本节包含下列主题：

[将 AFM 文件转换为 NTF 文件](converting-afm-files-to-ntf-files.md)

[将东亚版 AFM 文件转换为 NTF 文件](converting-east-asian-afm-files-to-ntf-files.md)

[安装 Pscript 微型驱动程序](installing-a-pscript-minidriver.md)

[PostScript 打印机标准功能](postscript-printer-driver-standard-features.md)

[Pscript 打印机微型驱动程序版本控制](pscript-printer-minidriver-versioning.md)

[Pscript 装钉支持](pscript-support-for-stapling.md)

[AddEuro](addeuro.md)

[TrueGray](truegray.md)

 

 




