---
title: 数据传输
description: 数据传输
ms.assetid: 55ef8125-40d3-44f3-8520-cc3a0912c3d2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ccead64857af5882fbe605e3c6c5d210aa25a6df
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364591"
---
# <a name="data-transfers"></a>数据传输





WIA 微型驱动程序的主要用途是将数据从设备传输到应用程序。 用于相机的数据可能以前捕获的图片、 音频或视频剪辑。 扫描程序，设备可能需要将数据传输，因为它将扫描程序获取它。

在操作系统中 Windows Vista，WIA 有两种方法来将数据从设备传输到应用程序前, 两者都基于[TYMED](understanding-tymed.md)。 第一种是内存中传输，该设备会返回 WIA 服务的图像数据的带区。 第二种方法是文件传输到 WIA 服务。 请注意 WIA 服务接收数据并将其转发给请求的应用程序。

在 Windows Vista 中，新的传输类型有：**IStream**-基于传输。 此传输模型依赖两个接口 (**IWiaItem2**并**IWiaDevMgr2**) 的是 Windows Vista 的新增功能。 （这两个接口描述了 Microsoft Windows SDK 文档中。）还有一个兼容性层，使 Windows Vista 和旧驱动程序和应用程序之间的有限的交互。 此兼容性层都有一些限制中, 讨论[实现兼容性与 IStream 传输](achieving-compatibility-with-istream-transfers.md)部分。

本部分包含以下主题：

[内存中传输](in-memory-transfers.md)

[文件传输](file-transfers.md)

[IStream 数据传输](istream-data-transfers.md)

有关数据传输的详细信息，请参阅[WIA 应用程序传输数据](transferring-data-to-a-wia-application.md)。

 

 




