---
title: WIA 数据项
description: WIA 数据项
ms.assetid: 3ce01393-4a0b-4b70-8087-abe989aa00a9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a3da29a7fcd005bf354f9ded4185c81962b803d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354865"
---
# <a name="wia-data-item"></a>WIA 数据项





本主题适用于 Windows Vista 和更高版本。

可用于将数据传输的任何项被视为数据项目。 这包括与标记的项**WiaItemTypeProgrammableDataSource**标志。 任何项标记有**WiaItemTypeTransfer**标志可以公开传输数据的功能。 设置了此标志的任何项必须提供以下 WIA 属性：

[**WIA\_IPA\_访问\_权限**](https://msdn.microsoft.com/library/windows/hardware/ff551518)

[**WIA\_IPA\_ITEM\_SIZE**](https://msdn.microsoft.com/library/windows/hardware/ff551594)

[**WIA\_IPA\_缓冲区\_大小**](https://msdn.microsoft.com/library/windows/hardware/ff551527)

[**WIA\_IPA\_格式**](https://msdn.microsoft.com/library/windows/hardware/ff551553)

[**WIA\_IPA\_PREFERRED\_FORMAT**](https://msdn.microsoft.com/library/windows/hardware/ff551623)

[**WIA\_IPA\_TYMED**](https://msdn.microsoft.com/library/windows/hardware/ff551656)

[**WIA\_IPA\_FILENAME\_EXTENSION**](https://msdn.microsoft.com/library/windows/hardware/ff551549)

可编程数据源项标记有**WiaItemTypeTransfer**标志必须提供这些 WIA 属性。 例如，平板扫描仪项必须具有这些属性，以正确配置的数据传输。

WIA 数据项可能具有其他属性，具体取决于项的标志设置。 例如，WIA 项标记有**WiaItemTypeImage**标志应具有特定于映像的信息的属性，例如[ **WIA\_IPA\_深度**](https://msdn.microsoft.com/library/windows/hardware/ff551546)并[ **WIA\_IPA\_数\_OF\_行**](https://msdn.microsoft.com/library/windows/hardware/ff551611)。

 

 




