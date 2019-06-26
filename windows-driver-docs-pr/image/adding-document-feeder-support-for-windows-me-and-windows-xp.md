---
title: 为 Windows Me 和 Windows XP 添加文档送纸器支持
description: 为 Windows Me 和 Windows XP 添加文档送纸器支持
ms.assetid: f3be94fa-6fb7-45de-a3ce-f3d173e802cf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e337db52a16eb9d732e088b5112e57ba603ea0e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375943"
---
# <a name="adding-document-feeder-support"></a>添加文档送纸器支持

文档送纸器是一项附加到或内置的扫描程序自动送入纸质文档中要扫描的位置。 对于具有文档送纸器扫描程序，该功能是公开并添加了以下列表中包含的属性控制。 对于 Windows Me 和 Windows XP，以下属性都位于根项：

- [**WIA\_DPS\_HORIZONTAL\_SHEET\_FEED\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-horizontal-sheet-feed-size)
- [**WIA\_DPS\_VERTICAL\_SHEET\_FEED\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-vertical-sheet-feed-size)
- [**WIA\_DPS\_MIN\_HORIZONTAL\_SHEET\_FEED\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-min-horizontal-sheet-feed-size)
- [**WIA\_DPS\_MIN\_VERTICAL\_SHEET\_FEED\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-min-vertical-sheet-feed-size)
- [**WIA\_DPS\_表\_送纸器\_注册**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-sheet-feeder-registration)
- [**WIA\_DPS\_文档\_处理\_功能**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-capabilities)
- [**WIA\_DPS\_文档\_处理\_状态**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-status)
- [**WIA\_DPS\_文档\_处理\_选择**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-select)
- [**WIA\_DPS\_PAGES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-pages)

对于 Windows Me 和 Windows XP，以下可选文档送纸器属性都位于子项目：

- [**WIA\_DPS\_PAGE\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-page-size)
- [**WIA\_DPS\_PAGE\_WIDTH**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-page-width)
- [**WIA\_DPS\_PAGE\_HEIGHT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-page-height)
- [**WIA\_IP\_方向**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-orientation)

如果设备具有平板、 文档送纸器和双面打印器，该驱动程序将报告 WIA\_DPS\_文档\_处理\_功能属性设置为 (源 |平面 |DUP)。 请确保 WIA 的有效值\_DPS\_文档\_处理\_选择设置正确。

例如，假设应用程序想要从文档送纸器中执行双工扫描三个页面。 若要实现此目的，应用程序设置 WIA\_DPS\_文档\_处理\_选择属性 (送纸器 |双工），并设置 WIA\_DPS\_页属性设置为 3。 如果该应用程序计划第一次扫描的页的前面，则应设置 WIA\_DPS\_文档\_处理\_选择属性 (送纸器 |双工 |前\_第一个)。 此操作完成后，应用程序应导航到子项目，它应从中请求数据传输。 微型驱动程序所报告的送纸器中的第一页前面的第一页上两个，因为该页面状态的页和第三页为送纸器中的第二个页面的前面。

请务必记住，是否设备具有文档送纸器，它必须支持文档送纸器属性。

## <a name="acquiring-data-from-a-document-feeder"></a>获取文档送纸器中的数据

有几个必须在实现中进行的更改[ **IWiaMiniDrv::drvAcquireItemData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)当扫描程序获取文档送纸器中的映像的方法。

1. 应用程序读取 WIA\_DPS\_文档\_处理\_功能属性来确定扫描程序是否支持扫描使用文档送纸器。
1. 应用程序读取 WIA\_DPS\_文档\_处理\_选择属性，以确定是否将扫描程序配置为使用文档送纸器扫描。
1. 应用程序确定是否存在纸张文档送纸器中阅读 WIA\_DPS\_文档\_处理\_状态。 如果存在缺纸的送纸器中，则设置 WIA\_DPS\_文档\_处理\_状态设置为适当的状态代码和返回 WIA\_错误\_纸张\_从空**IWiaMiniDrv::drvAcquireItemData**立即发生收购后。
1. 检查 WIA\_DPS\_页属性来确定扫描行为。 如果此属性为零，扫描的所有页面，直到送纸器为空。 如果为正数，扫描仅由 WIA 中包含的值指示的页面数\_DPS\_页属性。
1. 通过控制循环、 持续扫描，并将数据 （一次一页） 发送到 WIA 应用程序，通过调用扫描请求的页面数[ **IWiaMiniDrvCallBack::MiniDrvCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvcallback-minidrvcallback)方法。 下面的代码示例显示了这可能工作原理：

    ```cpp
    for(int x=1; x=Pagecount; x++)
    {
        \\ Tell scanner to scan an image.
        \\ Receive image data from scanner.
        \\ Send the just-scanned image to the registered application.
    }
    ```

1. 如果[ **WIA\_IPA\_TYMED** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-tymed)设置为 TYMED\_回调或 TYMED\_多页\_回调，则额外的消息 (IT\_MSG\_新建\_页) 扫描一页后和下一个要扫描之前必须发送。 这是通过调用[ **wiasSendEndOfPage** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiassendendofpage) WIA 服务实用工具函数。

文档送纸器驱动程序返回的页面数取决于设置 WIA\_DPS\_页属性。

## <a name="if-wiadpspages-is-zero"></a>如果 WIA\_DPS\_页为零

1. 如果扫描程序不能扫描的第一页，请立即返回错误代码。 这包括纸和缺纸扫描程序的运行时。
1. 如果扫描程序已成功扫描的第一页和能够继续扫描，但已用完纸张，则返回成功代码 WIA\_状态\_最终\_OF\_媒体。 这会指示应用程序传输已成功，但在扫描程序已用完纸张。 某些应用程序响应 WIA\_错误\_纸张\_空相同的方式，就像为 WIA\_状态\_最终\_OF\_媒体。
1. 如果扫描程序已成功扫描的第一页和能够继续扫描，但遇到一个错误，不会导致数据丢失，返回 WIA\_状态\_最终\_OF\_媒体。 这样，应用程序恢复并保存扫描在错误发生之前任何页。 立即扫描程序已正确地从失败中恢复之前，任何后续扫描应返回一个错误代码。
1. 如果扫描程序已成功扫描的第一页和能够继续扫描，但遇到一个错误，会导致数据丢失，请立即返回错误代码。

## <a name="if-wiadpspages-is-positive"></a>如果 WIA\_DPS\_页为正

1. 所有规则的 WIA\_DPS\_页面是零个应用。
1. 如果扫描程序用尽了纸张之前请求的页面数进行扫描，则返回 WIA\_状态\_最终\_OF\_媒体。 这样，应用程序来关闭扫描的会话，因此保留了它已成功扫描的页数。 某些应用程序响应 WIA\_错误\_纸张\_空相同的方式，就像为 WIA\_状态\_最终\_OF\_媒体。
