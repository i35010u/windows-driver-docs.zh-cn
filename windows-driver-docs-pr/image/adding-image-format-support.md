---
title: 添加图像格式支持
description: 添加图像格式支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc45f5835a0107b113c73b425ef6d02f876897da
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808275"
---
# <a name="adding-image-format-support"></a>添加图像格式支持





WIA 微型驱动程序在 [**IWiaMiniDrv：:D rvgetwiaformatinfo**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetwiaformatinfo) 方法中报告 wia 服务的图像格式。

### <a name="implementing-iwiaminidrvdrvgetwiaformatinfo"></a><a href="" id="implementing-iwiaminidrv-drvgetwiaformatinfo"></a>实现 IWiaMiniDrv：:d rvGetWiaFormatInfo

WIA 服务调用 **IWiaMiniDrv：:D rvgetwiaformatinfo** 方法，以获取 WIA 设备支持的 TYMED 和格式对。

WIA 驱动程序应分配内存 (以存储在此 WIA 驱动程序中并通过此 WIA 驱动程序释放，) 以包含一个 WIA \_ 格式 \_ 信息结构数组 (在 Microsoft Windows SDK 文档) 中进行了介绍。 指向 WIA 驱动程序分配的内存的指针应传递给 *ppwfi*。 这不是直接执行的，而是使用指向指针的指针。 在下面的示例中， *ppwfi* 是通过 m WIAFormatInfo 0 的地址设置的 \_ \[ \] ，后者反过来计算为结构的第一个成员的地址。

需要注意的是，WIA 服务无法释放此内存。 WIA 驱动程序负责管理此已分配的内存。

WIA 驱动程序应写入 *pcelt* 参数指向的内存位置中分配的结构数。

WIA 设备应将 WIA 格式信息结构的 **guidFormatID** 成员 \_ 设置 \_ 为图像格式 GUID。 设备应将此结构的 **lTymed** 成员设置为与图像格式 GUID 关联的 TYMED 值：

有效的 TYMED 值 (也称为 "媒体类型" ) ：

TYMED \_ 文件

TYMED \_ 多页 \_ 文件

TYMED \_ 回调

TYMED \_ 多页 \_ 回调

下面的示例演示了 IWiaMiniDrv 的实现 [**：:D rvgetwiaformatinfo**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetwiaformatinfo)：

```cpp
HRESULT _stdcall CWIADevice::drvGetWiaFormatInfo(
  BYTE            *pWiasContext,
  LONG            lFlags,
  LONG            *pcelt,
  WIA_FORMAT_INFO **ppwfi,
  LONG            *plDevErrVal)
{
    //
    // If the caller did not pass in the correct parameters,
    // then fail the call with E_INVALIDARG.
    //

    if ((!pWiasContext)||(!plDevErrVal)||(!pcelt)||(!ppwfi)) {
        return E_INVALIDARG;
    }

    //
    // check if WIA_FORMAT_INFO array has been initialized.
    //
    // NOTE: m_WIAFormatInfo is a member variable that has been
    //       defined as    WIA_FORMAT_INFO m_WIAFormatInfo[2];
    //
    //

    if (m_WIAFormatInfo[0].lTymed == TYMED_NULL) {

        //
        // add all supported formats and corresponding TYMED values
        // here
        //

        m_WIAFormatInfo[0].guidFormatID = WiaImgFmt_MEMORYBMP;
        m_WIAFormatInfo[0].lTymed       = TYMED_CALLBACK;

        m_WIAFormatInfo[1].guidFormatID = WiaImgFmt_BMP;
        m_WIAFormatInfo[1].lTymed       = TYMED_FILE;
    }

    *plDevErrVal = 0;
    *ppwfi = &m_WIAFormatInfo[0];
    *pcelt = 2; // number of formats in returned array

    return S_OK;
}
```

 

