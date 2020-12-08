---
title: 数据传输
description: 数据传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 184f22dac1cfe59cc44b31e632e4f03b60e35b8e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832977"
---
# <a name="data-transfers"></a>数据传输





WIA 微型驱动程序的主要用途是将数据从设备传输到应用程序。 对于照相机，数据可能是先前捕获的图片、音频或视频剪辑。 对于扫描仪，设备可能需要在从扫描程序获取数据时传输数据。

在 Windows Vista 之前的操作系统中，WIA 具有两种将数据从设备传输到应用程序的方法，这两种方法都基于 [TYMED](understanding-tymed.md)。 第一种是内存中的传输，其中设备将带区数据返回到 WIA 服务。 第二种方法是将文件传输到 WIA 服务。 请注意，WIA 服务接收了数据并将其转发到请求的应用程序。

在 Windows Vista 中，可以使用一种新的传输类型：基于 **IStream** 的传输。 此传输模型依赖于 Windows Vista 的新)  (**IWiaItem2** 和 **IWiaDevMgr2** 的两个接口。 Microsoft Windows SDK 文档中介绍了这两个接口 (。 ) 提供了一个兼容层，使得 Windows Vista 和旧驱动程序与应用程序之间的交互受到限制。 此兼容性层有一些限制，这在 " [实现与 IStream 传输的兼容性](achieving-compatibility-with-istream-transfers.md) " 部分中进行了讨论。

本节包含下列主题：

[内存中传输](in-memory-transfers.md)

[文件传输](file-transfers.md)

[IStream 数据传输](istream-data-transfers.md)

有关数据传输的详细信息，请参阅 [将数据传输到 WIA 应用程序](transferring-data-to-a-wia-application.md)。

 

 




