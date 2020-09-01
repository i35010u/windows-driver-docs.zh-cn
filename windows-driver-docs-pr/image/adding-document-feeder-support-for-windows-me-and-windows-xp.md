---
title: 为 Windows Me 和 Windows XP 添加文档送纸器支持
description: 为 Windows Me 和 Windows XP 添加文档送纸器支持
ms.assetid: f3be94fa-6fb7-45de-a3ce-f3d173e802cf
ms.date: 07/06/2020
ms.localizationpriority: medium
ms.openlocfilehash: 12a3af1d680d8dd0468485a724083c7aa2c0c058
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191974"
---
# <a name="adding-document-feeder-support"></a>添加文档送纸器支持

文档送纸器是指附加到扫描程序中或内置在扫描位置的扫描程序的单元。 对于带有文档送纸器的扫描仪，通过添加以下列表中包含的属性，可公开和控制该功能。 对于 Windows Me 和 Windows XP，以下属性位于根项上：

- [**WIA \_ DPS \_ 水平 \_ 工作 \_ 源 \_ 大小**](./wia-dps-horizontal-sheet-feed-size.md)

- [**WIA \_ DPS \_ 垂直 \_ 工作 \_ 源 \_ 大小**](./wia-dps-vertical-sheet-feed-size.md)

- [**WIA \_ DPS \_ 最小 \_ 水平 \_ 页面 \_ 源 \_ 大小**](./wia-dps-min-horizontal-sheet-feed-size.md)

- [**WIA \_ DPS \_ 最小 \_ 垂直 \_ 纸张 \_ 馈送 \_ 大小**](./wia-dps-min-vertical-sheet-feed-size.md)

- [**WIA \_ DPS \_ SHEET \_ 送纸器 \_ 注册**](./wia-dps-sheet-feeder-registration.md)

- [**WIA \_ DPS \_ 文档 \_ 处理 \_ 功能**](./wia-dps-document-handling-capabilities.md)

- [**WIA \_ DPS \_ 文档 \_ 处理 \_ 状态**](./wia-dps-document-handling-status.md)

- [**WIA \_ DPS \_ 文档 \_ 处理 \_ 选择**](./wia-dps-document-handling-select.md)

- [**WIA \_ DPS \_ 页面**](./wia-dps-pages.md)

对于 Windows Me 和 Windows XP，以下可选的文档送纸器属性位于子项上：

- [**WIA \_ DPS \_ 页面 \_ 大小**](./wia-dps-page-size.md)

- [**WIA \_ DPS \_ 页面 \_ 宽度**](./wia-dps-page-width.md)

- [**WIA \_ DPS \_ 页面 \_ 高度**](./wia-dps-page-height.md)

- [**WIA \_ IP \_ 方向**](./wia-ips-orientation.md)

如果设备具有平板、文档送纸器和双面打印器，则驱动程序会将 "WIA \_ DPS \_ 文档 \_ 处理功能" 属性报告 \_ 为 `FEED | FLAT | DUP` 。 请确保 \_ 正确设置了 WIA DPS \_ 文档处理的 \_ 有效值 \_ 。

例如，假设某个应用程序要对文档送纸器执行三个页面的双工扫描。 若要完成此操作，应用程序会将 WIA \_ DPS \_ 文档 \_ 处理 \_ 选择属性设置为 (送纸器 |双工) ，并将 "WIA \_ DPS \_ PAGES" 属性设置为3。 如果应用程序打算首先扫描页面正面，则应将 "WIA \_ DPS \_ 文档 \_ 处理选择属性" 设置 \_ 为 `FEEDER | DUPLEX | FRONT\_FIRST` 。 完成此操作后，应用程序应导航到从中请求数据传输的子项。 微型驱动程序报告送纸器中第一页的正面为第一页，该页的背面为第2页，进纸器中第二页的正面为第三页。

请务必记住，如果设备有文档送纸器，则必须支持文档送纸器属性。

## <a name="acquiring-data-from-a-document-feeder"></a>从文档送纸器中获取数据

当扫描程序从文档送纸器获取图像时，必须在 [**IWiaMiniDrv：:D rvacquireitemdata**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata) 方法的实现中进行一些更改。

1. 应用程序读取 "WIA \_ DPS \_ 文档 \_ 处理 \_ 功能" 属性，以确定扫描程序是否支持使用文档送纸器进行扫描。

1. 应用程序读取 WIA \_ DPS \_ 文档 \_ 处理 \_ 选择属性，以确定是否已将扫描仪配置为使用文档送纸器进行扫描。

1. 应用程序通过阅读 WIA \_ DPS \_ 文档 \_ 处理状态确定文档送纸器中是否有纸张 \_ 。 如果进纸器中没有纸张，请将 WIA \_ DPS \_ 文档 \_ 处理状态设置 \_ 为正确的状态代码，并 \_ \_ \_ 从 **IWiaMiniDrv：:d rvacquireitemdata** 立即返回 wia 错误纸张，并在收购后立即返回。

1. 检查 "WIA \_ DPS \_ 页" 属性以确定扫描行为。 如果此属性为零，则扫描所有页面，直到进纸器为空。 如果该属性为正值，则仅扫描 "WIA DPS 页" 属性中包含的值所指示的页数 \_ \_ 。

1. 通过调用 [**IWiaMiniDrvCallBack：： MiniDrvCallback**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvcallback-minidrvcallback) 方法，通过控制循环来扫描请求的页数，每次) 到 WIA 应用程序时，继续扫描并发送数据 (一页。 下面的代码示例演示如何执行此操作：

    ```cpp
    for(int x=1; x=Pagecount; x++)
    {
        \\ Tell scanner to scan an image.
        \\ Receive image data from scanner.
        \\ Send the just-scanned image to the registered application.
    }
    ```

1. 如果 [**WIA \_ IPA \_ TYMED**](./wia-ipa-tymed.md) 设置为 TYMED \_ 回调或 TYMED \_ 多页 \_ 回调，则在 \_ \_ 扫描一页后，必须发送一条额外的消息)  (消息新建页面，然后再 \_ 扫描下一个页面。 这是通过调用 [**wiasSendEndOfPage**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassendendofpage) WIA 服务实用函数来完成的。

文档送纸器驱动程序返回的页数取决于 "WIA \_ DPS 页" 属性的设置 \_ 。

## <a name="if-wia_dps_pages-is-zero"></a>如果 WIA \_ DPS \_ 页为零

1. 如果扫描程序无法扫描第一页，则立即返回错误代码。 这包括卡纸以及扫描程序缺纸。

1. 如果扫描程序成功扫描第一页，但仍可继续扫描但已用完纸张，则返回媒体的成功代码 \_ WIA \_ 状态 \_ 结束 \_ 。 这会向应用程序发出信号，指示传输已成功，但扫描程序已用完纸张。 某些应用程序会以 \_ 与 \_ \_ wia 状态结尾相同的方式来响应 wia 错误纸张 \_ \_ \_ \_ 。

1. 如果扫描程序成功扫描第一页，但仍能继续扫描，但遇到不会导致数据丢失的错误，则将返回 WIA \_ 状态 \_ 结束 \_ 的 \_ 媒体。 这样，应用程序便可以恢复并保存在错误发生之前扫描的任何页。 任何后续扫描都应立即返回错误代码，直到扫描仪正确地从故障中恢复为止。

1. 如果扫描程序成功扫描第一页并能够继续扫描，但遇到导致数据丢失的错误，则立即返回错误代码。

## <a name="if-wia_dps_pages-is-positive"></a>如果 WIA \_ DPS \_ 页为正数

1. WIA \_ DPS \_ 页为零的所有规则都适用。

1. 如果扫描程序在扫描请求的页数之前缺纸，则返回 "WIA \_ 状态结束" \_ \_ \_ 。 这允许应用程序关闭扫描会话，从而保留已成功扫描的页数。 某些应用程序会以 \_ 与 \_ \_ wia 状态结尾相同的方式来响应 wia 错误 \_ 纸张 \_ \_ \_ 。