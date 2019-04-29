---
title: Pscript 微型驱动程序
description: Pscript 微型驱动程序
ms.assetid: b1108a6b-e0cc-413c-b3ea-53a1aa3156c0
keywords:
- PostScript 打印机驱动程序 WDK 打印，微型驱动程序
- Pscript WDK 打印，微型驱动程序
- 微型驱动程序 WDK Pscript
- 微型驱动程序 WDK Pscript 有关 Pscript 微型驱动程序
- PPD 文件 WDK 打印
- .ppd 文件
- NTF 文件
- .ntf 文件
- 东亚字体 WDK 打印
- 亚洲字体 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcac1bd853231bcb038c174216d8d6e87f08908c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376541"
---
# <a name="pscript-minidrivers"></a>Pscript 微型驱动程序





从.ppd 文件和.ntf 文件创建 Pscript 微型驱动程序。

### <a href="" id="ddk-ppd-files-gg"></a>PPD 文件

基于文本的 PostScript 打印机说明文件 （.ppd 文件） 描述 PostScript 打印机的特征。 Pscript 驱动程序适用于 Microsoft Windows 2000 及更高版本支持的与版本 4.3 从 Adobe Systems，Inc.的 PPD 规范兼容.ppd 文件Pscript 读取打印机的.ppd 文件，并将文本转换为二进制格式，为每次.ppd 文件发生更改时重新生成的.bpd 文件存储在本地。

### <a href="" id="ddk-ntf-files-gg"></a>NTF 文件

Windows 2000 和更高版本的字体文件 （.ntf 文件） 是用于描述设备字体的打印机支持的 Pscript 的二进制文件。

Microsoft 提供了名为 pscript.ntf，其中包含说明通常会遇到美国设备字体的默认.ntf 文件。 东亚打印机 Microsoft 设备字体还提供名为 pscrptfe.ntf，其中包含通常会遇到的东亚语言的说明的默认.ntf 文件。

此外，硬件供应商可以提供字体不受 pscript.ntf 设备字体的说明。 可以通过创建这些字体描述[将 AFM 文件转换为 NTF 文件](converting-afm-files-to-ntf-files.md)。 自定义，打印机的型号特定.ntf 文件可以安装为依赖文件中的列出这些[打印机 INF 文件](printer-inf-files.md)。 有关详细信息，请参阅[安装 Pscript 微型驱动程序](installing-a-pscript-minidriver.md)。

字体规格的第一个检查打印机的型号特定.ntf 文件，然后检查 pscript.ntf，并使用找到的第一个字体说明 Pscript 搜索。

本部分包含以下主题：

[将 AFM 文件转换为 NTF 文件](converting-afm-files-to-ntf-files.md)

[将东亚 AFM 文件转换为 NTF 文件](converting-east-asian-afm-files-to-ntf-files.md)

[安装 Pscript 微型驱动程序](installing-a-pscript-minidriver.md)

[PostScript 打印机标准功能](postscript-printer-driver-standard-features.md)

[Pscript 打印机微型驱动程序版本控制](pscript-printer-minidriver-versioning.md)

[装订 Pscript 支持](pscript-support-for-stapling.md)

[AddEuro](addeuro.md)

[TrueGray](truegray.md)

 

 




