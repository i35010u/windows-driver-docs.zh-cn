---
title: 为 Windows Me 和 Windows XP 添加文档送纸器支持
description: 为 Windows Me 和 Windows XP 添加文档送纸器支持
ms.assetid: f3be94fa-6fb7-45de-a3ce-f3d173e802cf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6aa09bef818282a8a0ca8b298b6327e8beedeecf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840911"
---
# <a name="adding-document-feeder-support"></a>添加文档送纸器支持

文档送纸器是指附加到扫描程序中或内置在扫描位置的扫描程序的单元。 对于带有文档送纸器的扫描仪，通过添加以下列表中包含的属性，可公开和控制该功能。 对于 Windows Me 和 Windows XP，以下属性位于根项上：

- [**WIA\_DP\_水平\_表\_源\_大小**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-horizontal-sheet-feed-size)
- [**WIA\_DP\_竖\_SHEET\_源\_大小**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-vertical-sheet-feed-size)
- [**WIA\_DPS\_MIN\_水平\_工作表\_源\_大小**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-min-horizontal-sheet-feed-size)
- [**WIA\_DPS\_MIN\_直排\_SHEET\_源\_大小**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-min-vertical-sheet-feed-size)
- [**WIA\_DPS\_SHEET\_送纸器\_注册**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-sheet-feeder-registration)
- [**WIA\_DPS\_文档\_处理\_功能**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-capabilities)
- [**WIA\_DPS\_文档\_处理\_状态**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-status)
- [**WIA\_DPS\_文档\_处理\_SELECT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-select)
- [**WIA\_DPS\_页**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-pages)

对于 Windows Me 和 Windows XP，以下可选的文档送纸器属性位于子项上：

- [**WIA\_DPS\_页\_大小**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-page-size)
- [**WIA\_DPS\_页\_宽度**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-page-width)
- [**WIA\_DPS\_页\_高度**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-page-height)
- [**WIA\_IP\_方向**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-orientation)

如果设备具有平板、文档送纸器和双面打印器，则驱动程序会将 WIA\_DPS\_文档\_处理\_功能属性作为源 |平面 |DUP）。 请确保正确设置了 WIA\_DPS\_文档\_\_处理的有效值。

例如，假设某个应用程序要对文档送纸器执行三个页面的双工扫描。 若要完成此操作，应用程序会将 WIA\_DPS\_文档\_处理设置\_选择属性设置为（进纸器 |双工），并将 WIA\_DPS\_PAGES 属性设置为3。 如果应用程序打算首先扫描页面正面，则应将 WIA\_DPS\_文档\_处理\_选择属性设置为（进纸器 |双工 |前面\_第一个）。 完成此操作后，应用程序应导航到从中请求数据传输的子项。 微型驱动程序报告送纸器中第一页的正面为第一页，该页的背面为第2页，进纸器中第二页的正面为第三页。

请务必记住，如果设备有文档送纸器，则必须支持文档送纸器属性。

## <a name="acquiring-data-from-a-document-feeder"></a>从文档送纸器中获取数据

当扫描程序从文档送纸器获取图像时，必须在[**IWiaMiniDrv：:D rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)方法的实现中进行一些更改。

1. 应用程序读取 WIA\_DPS\_文档\_处理\_功能属性，以确定扫描程序是否支持使用文档送纸器进行扫描。
1. 应用程序读取 WIA\_DPS\_文档\_处理\_选择属性，以确定是否已将扫描仪配置为使用文档送纸器进行扫描。
1. 应用程序通过阅读 WIA\_DPS\_文档\_处理\_状态来确定文档送纸器中是否存在纸张。 如果进纸器中没有纸张，请将 WIA\_DPS\_文档\_处理\_状态设置为正确的状态代码，并从 IWiaMiniDrv 中返回 WIA\_错误\_纸张\_空 **：** 在获取 rvacquireitemdata 后立即:d。
1. 检查 WIA\_DPS\_PAGES "属性以确定扫描行为。 如果此属性为零，则扫描所有页面，直到进纸器为空。 如果是正数，只扫描 WIA\_DPS\_PAGES 属性中包含的值所指示的页数。
1. 通过使用[**IWiaMiniDrvCallBack：： MiniDrvCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvcallback-minidrvcallback)方法控制循环、不断扫描和发送数据（一次一页）并将数据发送到 WIA 应用程序，扫描请求的页数。 下面的代码示例演示如何执行此操作：

    ```cpp
    for(int x=1; x=Pagecount; x++)
    {
        \\ Tell scanner to scan an image.
        \\ Receive image data from scanner.
        \\ Send the just-scanned image to the registered application.
    }
    ```

1. 如果[**WIA\_IPA\_TYMED**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-tymed)设置为 TYMED\_回叫或 TYMED\_多页\_回调，则必须在扫描一页后发送额外的消息（它\_"新\_" 页），，然后扫描下一个。 这是通过调用[**wiasSendEndOfPage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassendendofpage) WIA 服务实用函数来完成的。

文档送纸器驱动程序返回的页数取决于 WIA\_DPS\_PAGES 属性的设置。

## <a name="if-wia_dps_pages-is-zero"></a>如果 WIA\_DPS\_页为零

1. 如果扫描程序无法扫描第一页，则立即返回错误代码。 这包括卡纸以及扫描程序缺纸。
1. 如果扫描程序成功扫描第一页，但仍能继续扫描，但仍用完了纸张，则返回\_媒体\_结束\_\_状态的成功代码 WIA。 这会向应用程序发出信号，指示传输已成功，但扫描程序已用完纸张。 某些应用程序会响应 WIA\_错误\_纸张\_为空\_状态\_\_\_媒体。
1. 如果扫描程序成功扫描第一页，但仍能继续扫描，但遇到不会导致数据丢失的错误，则会将 WIA\_状态返回\_媒体\_结束\_。 这样，应用程序便可以恢复并保存在错误发生之前扫描的任何页。 任何后续扫描都应立即返回错误代码，直到扫描仪正确地从故障中恢复为止。
1. 如果扫描程序成功扫描第一页并能够继续扫描，但遇到导致数据丢失的错误，则立即返回错误代码。

## <a name="if-wia_dps_pages-is-positive"></a>如果 WIA\_DPS\_页为正

1. WIA\_DPS\_页的所有规则都适用。
1. 如果扫描程序在扫描请求的页数之前缺纸，请返回 WIA\_状态\_结束\_\_媒体。 这允许应用程序关闭扫描会话，从而保留已成功扫描的页数。 某些应用程序会响应 WIA\_错误\_纸张\_为空\_状态\_\_\_媒体的状态。
